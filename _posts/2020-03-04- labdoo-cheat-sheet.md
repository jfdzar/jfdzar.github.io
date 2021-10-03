---
bg: "tools.jpg"
layout: post
title:  Cheat Sheet Labdoo
crawlertitle: Cheat Sheet Labdoo
summary: Cheat Sheet Labdoo
date:   2020-03-04
categories: posts
tags: ['labdoo', 'linux','cheatsheet']
author: jfdzar
---

Good page with Linux command for sysadmins: helpful cheat sheet

https://haydenjames.io/90-linux-commands-frequently-used-by-linux-sysadmins/

* Check serial number
```bash
sudo dmidecode -s system-serial-number
```
* Check the Processor
```bash
lscpu
```
* Check the RAM
```bash
free -m
```
* Check the HDD
```bash
sudo fdisk -l
```
* Shred
```bash
shred /dev/sda -v -f
```
* Cambiar nombre de host
```bash
sudo nano /etc/hosts
sudo nano /etc/hostname
```
* Instalar Language Packages
```bash
sudo apt-get -y install `check-language-support -l fr`
du -h --max-depth=1 /Media/
```

Doing a manual restore through command line

First Shred
```bash
shred /dev/sda -v -f
```
Restore Image
```bash
ocs-sr -g auto -e1 auto -e2 -batch -r -icds -scr -j2 -p true restoredisk /home/partimag/PAE64_18_04_LTS_EN_250 sda
```

mount /dev/$source_disk /home/partimag
or directly take the image from there

Then try to do the following

```bash
ocssr=$(which ocs-sr)
$ocssr -g auto -e1 auto -e2 -batch -r -icds -scr -j2 -p true restoredisk "$IMAGEDIRTOINSTALL" $target_disk   

rootuuid=$(blkid |grep ext4 |awk -F'\"' '{print $2}')

echo "rootuuid = $rootuuid"
startpart=$(parted /dev/$target_disk print |grep ext4 |awk '{print $2}')
echo "Partition start at: $startpart" >>/root/labdoo_install.log
echo "UUID ROOT: $rootuuid" >>/root/labdoo_install.log
parted -s /dev/$target_disk rm 1


#Recreate sda1 larger and reset UUID and boot flag
parted -s -a optimal /dev/$target_disk mkpart primary ext4 -- "$startpart" -0
target_disk_1="${target_disk}1"
tune2fs /dev/$target_disk_1 -U "$rootuuid"
parted -s /dev/$target_disk set 1 boot on

#Fsck FS and resize
sleep 2
e2fsck -pf /dev/$target_disk_1
sleep 2
resize2fs /dev/$target_disk_1

#Write install.log
mount /dev/$target_disk_1 /mnt
cp /root/labdoo_install.log /mnt/root/labdoo_install.log
```