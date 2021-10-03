---
bg: "tools.jpg"
layout: post
title:  Cheat Sheet Raspberry Pi - Linux
crawlertitle: Cheat Sheet Raspberry Pi - Linux
summary: Cheat Sheet Raspberry Pi - Linux
date:   2020-02-27
categories: posts
tags: ['linux', 'raspberry', 'cheatsheet']
author: jfdzar
---

In this entry I would document some interesting linux commands to use in the raspberry pi

* history
To see the history of commands you typed
* crontab -e
Different for sudo and user
* ssh user@ipofthehost
To connect to the raspberry pi remotely from other laptop through ssh
    nohup python /path/to/test.py > output.log &
    Correr el script y guardar el output en output.log
    ps ax | grep test.py
    Ver que PID tiene el script de python
    kill PID
    Matar el proceso (PID = el numero)
    dmesg
    list of devices
    lsusb
    list of USB devices
    uname -r
    kernel of linux used
    find / -name "8192" -print
    look for "8192" in /
    lsmod
    check loaded modules
    mount -t cifs -o username=juan //server /localfolder
    mount network device need cifs-utils needs root
    smbpasswd -a osmc
    change samba password of osmc user
    rm -r foldername
    delete folder and its content
    Download file from ssh server
    scp pi@pisalamanca:/home/pi/ovpns/jfdzar_mobile.ovpn jfdzar_mobile.ovpn
    Check the disk usage of a directory
    du -h --max-depth=1 /Media/


