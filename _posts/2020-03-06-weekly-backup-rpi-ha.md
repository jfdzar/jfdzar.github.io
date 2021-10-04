---
bg: "tools.jpg"
layout: post
title:  Creating a weekly Backup Raspberry Pi - Homeassistant
crawlertitle: Creating a weekly Backup Raspberry Pi - Homeassistant
summary: Creating a weekly Backup Raspberry Pi - Homeassistant
date:   2020-03-06
categories: posts
tags: ['homeassistant','raspberry','linux']
author: jfdzar
---
Mounting net drives, creating backups is always a recurring topic I treat different in my different machines.

I will try to explain the approach I took with my Homeassistant Files which are installed in a Raspberry Pi.

I will create a bash script which will be executed with a cronjob every week to backup the important directories of the raspberry pi with rsync

Let's start!

First of all I created a file with the credentials of my network drive on /root/

```bash
sudo nano /root/.networkdrivecredentials
```

```bash
user=myuser
password=mypassword
```

and I make the file only accessible for root

```bash
sudo chmod 700 /root/.networkdrivecredentials
```

After that I check that the mounting of the drive with the credentials work

```bash
sudo mkdir /media/NETWORK-DRIVE

sudo mount.cifs //IP-NETWORK-DRIVE/MyFolder /media/NETWORK-DRIVE -o credentials=/root/.networkdrivecredentials
```

It worked!
Now the Script works more or less like this

- Check if the Network drive is mounted, if not mount it
- Rsync the needed directories
- Unmount the network drive

```bash
#!/bin/bash

if [ -d "/media/NETWORK-DRIVE/MyFolder" ]; then
    # Control will enter here if $DIRECTORY exists.
    echo "Drive mounted!"
else
    echo "Not Mounted"
    mount.cifs //IP-NETWORK-DRIVE/MyFolder /media/NETWORK-DRIVE -o credentials=/root/.networkdrivecredentials
fi

rsync -avzh /home/MyFolder/ /media/NETWORK-DRIVE/
sudo umount /media/NETWORK-DRIVE
```