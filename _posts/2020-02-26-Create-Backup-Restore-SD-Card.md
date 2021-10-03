---
bg: "tools.jpg"
layout: post
title:  Create a Backup or Restore SD Card
crawlertitle: Create a Backup or Restore SD Card
summary: Create a Backup or Restore SD Card
date:   2020-02-26
categories: posts
tags: ['linux', 'raspberry']
author: jfdzar
---

Source 1: https://thepihut.com/blogs/raspberry-pi-tutorials/17789160-backing-up-and-restoring-your-raspberry-pis-sd-card

Source 2: https://beebom.com/how-clone-raspberry-pi-sd-card-windows-linux-macos/

Using Linux
Before inserting the SD card into the reader on your Linux PC, run the following command to find out which devices are currently available:
    df -h
Check the difference and discover your Raspberry
The left column gives the device name of your SD card, and will look like '/dev/mmcblk0p1' or '/dev/sdb1'. The last part ('p1' or '1') is the partition number, but you want to use the whole SD card, so you need to remove that part from the name leaving '/dev/mmcblk0' or '/dev/sdb' as the disk you want to read from.
Open a terminal window and use the following to backup your SD card:
    sudo dd if=/dev/sdb of=~/SDCardBackup.img
As on the Mac, the dd command does not show any feedback so you just need to wait until the command prompt re-appears.
To restore the image, do exactly the same again to discover which device is your SD card.  As with the Mac, you need to unmount it first, but this time you need to use the partition number as well (the 'p1' or '1' after the device name).  If there is more than one partition on the device, you will need to repeat the umount command for all partition numbers.  For example, if the df -h shows that there are two partitions on the SD card, you will need to unmount both of them:
    sudo umount /dev/sdb1
    sudo umount /dev/sdb2
Now you are able to write the original image to the SD drive:
    sudo dd bs=4M if=~/SDCardBackup.img of=/dev/sdb
The bs=4M option sets the 'block size' on the SD card to 4Meg.  If you get any warnings, then change this to 1M instead, but that will take a little longer to write.
Again, wait while it completes.  Before ejecting the SD card, make sure that your Linux PC has completed writing to it using the command:
    sudo sync 