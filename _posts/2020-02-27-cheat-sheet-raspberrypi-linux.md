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

*  To see the history of commands you typed
```bash
history
```
*  Different for sudo and user
```bash
crontab -e
```
*  To connect to the raspberry pi remotely from other laptop through ssh
```bash
ssh user@ipofthehost
```
* Correr el script y guardar el output en output.log
```bash
nohup python /path/to/test.py > output.log &
```
* Ver que PID tiene el script de python
```bash
ps ax | grep test.py
```
* Matar el proceso (PID = el numero)
```bash
kill PID
```
* list of devices
```bash
dmesg
```
* list of USB devices
```bash
lsusb
```
* kernel of linux used
```bash
uname -r
```
* look for "8192" in /
```bash
find / -name "8192" -print
```
* check loaded modules
```bash
lsmod
```
* mount network device need cifs-utils needs root
```bash
mount -t cifs -o username=juan //server /localfolder
```
* change samba password of osmc user
```bash
smbpasswd -a osmc
```
* delete folder and its content
```bash
rm -r foldername
```
* Download file from ssh server
```bash
scp pi@pisalamanca:/home/pi/ovpns/jfdzar_mobile.ovpn jfdzar_mobile.ovpn
```
* Check the disk usage of a directory
```bash
du -h --max-depth=1 /Media/
```


