---
bg: "tools.jpg"
layout: post
title:  Maintenance WD My Cloud
crawlertitle: Maintenance WD My Cloud
summary: Maintenance WD My Cloud
date:   2021-11-28
categories: posts
tags: ['wd-mycloud','linux']
author: jfdzar
---

I have a WD My Cloud disk as a Network Storage at home.
WD My Cloud come with a customize Linux version which can do all kind of fancy stuff which is mainly not usefull and it just keep the drive working all day.

I have always had the device connected to the LAN but blocked from Internet through my router as I want to avoid automatic updates and extrange people accessing my data.

It has been working pretty well..but as usual I was running out of space.... So I start copying files to other drives as backup and deleting it from the main drive, this started my journey to stop not usefull services from the drive and run daemonds in the background to copy files from one drive to another


# 1. Stop unused Services
The first thing I did was to stop the services which were consuming most of the CPU Power of the WD My Cloud. There is a lot of stuff in internet and a some people did a great research

## 1.1 Stop Services Manually
First option is to stop service manually, as described here below.
But in every start they would start anoying again...

[Source 1](https://gist.github.com/v0lkan/7db81cce6d92ecc70588c7d83c75f655)

```bash
/etc/init.d/wdmcserverd stop
/etc/init.d/wdphotodbmergerd stop

ps aux | grep wd

```

# 1.2 Stop Services on boot up
This guy had the final solution!
I have copied all the post below, as maybe they could delete the thread in the forum... But I leave a link to the original post.

My drive has a different firmware version and the display of the capacity was working from the beginning, that's why I did not do the second part of the solution

[Copy directly from Source, in case post deleted](https://community.wd.com/t/how-to-permanently-disable-wdmcserverd-and-wdphotodbmergerd/135878)

Thought i would share how to permanently disable wdmcserverd and wdphotodbmergerd (media scanning and thumbnail generation services) since a lot of people seem to be having similar issues with 100% CPU usage and the drive not sleeping.

First step was to prevent the services from starting on boot.

You will need to enable ssh and login to your drive using the default password and navigate to /etc/init.d

```bash
WDMyCloud:~#
cd /etc/init.d
ls
```

Here you will find the init scripts for the various services. Edit “wdmcserverd” and “wdphotodbmergerd”. All you need to do here is add an “exit 0” after the first line.

```bash
pico wdmcserverd
pico wdphotodbmergerd
```

Both pico and vi are available on the WD MyCloud, so either will do. The first lines of both files should look now like this:

```bash
#!/bin/sh
exit 0
```

After saving the files you can reboot the drive and that should be it.

Except that you may notice the web interface now no longer shows the drive capacity.

To fix this we need to hunt around a bit more in the code of the AXAJ/PHP web interface which is all accessible via ssh once again.

If you want to skip to the solution just got the sections labelled (1.) and (2.) below. What follows is an walk-through of how i did it.

Log in via ssh again, and navigate to the web root:

```bash
cd /var/www/htdocs
```

At this point i started looking around for various likely files, but a faster way would be grepping for keywords like “capacity”, “storage”, and “usage” as in “grep -R capacity”.

In any case a educated guesses at the fairly logical file structure and this led me to find “gCapacity” and “gUsage” in “UI/js/global.js” so i knew where things were going to end up. There was also a function as follows:

```php
function get_storage_capacity() {
    $.ajaxAPI({
        "url": "storage_usage",
        "success": function(data) {
            return parseInt(data.storage_usage.size);
        }
    });
}
```

Since its a single page HTML5 application meant there had to be a REST api around somewhere, and this variable tells us:

```php
var apiUrlPrefix = "/api/2.1/rest/";
```

Typing the full url “http://[hostname]/api/2.1/rest/storage_usage” into my browser i could see the error message was that an uncaught exception was being thrown in place of the XML.

So i hunted around for the api code, there is an “api/rest” folder in the root of “/var/www/htdocs” but that only contained a single index.php file. Further up the tree we find a “rest-api” folder in the root of “/var/www” which contains some promising looking structure. After a “grep -R storage_usage” from this folder i located the PHP file (1.) In this file, knowing that we have disabled the media scanning service i commented out the line which was trying to calculate media breakdown.

1.)

```bash
pico /var/www/rest-api/api/Storage/src/Storage/Controller/Usage.php
```

```php
//$result = $storageUsageObj->calculateMediaBreakdown($result);
```

As indicated by the “use Storage\Model;” at the top and the “$storageUsageObj = new Model\Usage();” declaration there is a corresponding Model.php somewhere. We also see an interesting description of how the usage is calculated to account for reserved space and an example of the correct XML output if no exception is thrown.

I expected the usage to come from parsing a “df” command output and that’s correct.

Editing the model file (2.), the only two lines i needed to change appeared to be references to the media database object which i guessed was now throwing an exception.

2.)

```bash
pico /var/www/rest-api/api/Storage/src/Storage/Model/Usage.php
```

```php
public function __construct($dbPath = null) {
	//$this->mediaDb = openMediaDb($dbPath);
	$this->dbAccess = new \DBAccess();
}
```
```php
public function __destruct() {
	//closeMediaDb($this->mediaDb);
}
```

With that we are done, so restart apache and load the web interface to see the new capacity correctly calculated.

```bash
cd /etc/init.d
./apache2 restart
```

# 2. Run Services on the Background
So the initial idea was to backup information which I usually do not change/access to external drives to avoid having things just in one place. But the linux distro of WD My Cloud does not have systemctl which is what I know how to use.

I had to do some reasearch and after lot's of tries I discovered I can use SysVinit
[How to proper start/stop services](https://blog.frd.mn/how-to-set-up-proper-startstop-services-ubuntu-debian-mac-windows/)

In my particular case, what I did was

First create a new file in /etc/init.d

'''bash
sudo nano /etc/init.d/mydrive-backup
'''

Mainly structured like this

```bash
#!/bin/bash
rsync -avzh "SourcePath" "DestinationPath" --progress > "LogFilePath" &
exit 0
```

then I just start the service

```bash
service mydrive-backup start
```

And I check in the log file that it was running. Done!

If at some point I want to do a weekly backup from other drives I would use a cronjob to start the service :)

# 3. Extra Stuff
There was some critical steps during my day doing all this stuff where I though my drive was dead. So I had to look up this stuff:
[How to Reset WD My Cloud](https://support-en.wd.com/app/answers/detail/a_id/24022)

I keep it here just in case for the future!