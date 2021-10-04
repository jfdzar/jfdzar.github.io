---
bg: "tools.jpg"
layout: post
title:  Creating a systemd service in Linux
crawlertitle: Creating a systemd service in Linux
summary: Creating a systemd service in Linux
date:   2020-03-14
categories: posts
tags: ['linux']
author: jfdzar
---

I was running python scripts on the raspberry pi quite complicating everything.

I was running a bash script which was checking if the script was running and if it was not running it would start it

But it was not correctly working, and had problems when booting

I decided to run the python script as a systemd service

I followed [this guide](https://www.raspberrypi.org/documentation/linux/usage/systemd.md)

I create myservice.service

```bash
[Unit]
Description=My service
After=network.target

[Service]
ExecStart=/usr/bin/python3 -u main.py
WorkingDirectory=/home/pi/myscript
StandardOutput=inherit
StandardError=inherit
Restart=always
User=pi

[Install]
WantedBy=multi-user.target
```

And copy it to /etc/systemd/system as root, for example:

```bash
sudo cp myscript.service /etc/systemd/system/myscript.service
```

Once this has been copied, you can attempt to start the service using the following command:

```bash
sudo systemctl start myscript.service
```

Stop it using following command:
```bash
sudo systemctl stop myscript.service
```

When you are happy that this starts and stops your app, you can have it start automatically on reboot by using this command:

```bash
sudo systemctl enable myscript.service
```
 
I wanted also to be able to restart periodically so I followed [this post in stack](https://stackoverflow.com/questions/31055194/how-can-i-configure-a-systemd-service-to-restart-periodically)

```bash
[Service]
Restart=always
RuntimeMaxSec=604800
``` 

At the moment looks like working lets see 