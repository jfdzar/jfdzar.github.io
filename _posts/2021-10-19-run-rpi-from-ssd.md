---
bg: "tools.jpg"
layout: post
title:  Run Raspberry Pi from USB Drive
crawlertitle: Run Raspberry Pi from USB Drive
summary: Run Raspberry Pi from USB Drive
date:   2021-10-19
categories: posts
tags: ['linux','raspberry']
author: jfdzar
---

[Source 1](https://www.thesecmaster.com/three-different-ways-to-boot-a-raspberry-pi-from-a-usb-drive/)

First prepare the Hard Drive following a previous guide
[Source 2](https://www.thesecmaster.com/how-to-partition-and-format-the-hard-drives-on-raspberry-pi/)



Copy Output of commands in Rpi


pi@pihumboldt:~ $ sudo blkid
/dev/mmcblk0p1: LABEL_FATBOOT="boot" LABEL="boot" UUID="7581-8A48" TYPE="vfat" PARTUUID="3fe6837a-01"
/dev/mmcblk0p2: LABEL="rootfs" UUID="fa37d505-e741-4d35-bcec-4580aef395e1" TYPE="ext4" PARTUUID="3fe6837a-02"
/dev/sda: LABEL="rpi" UUID="b2d4f8fa-0dc7-42d0-a4e3-b94db18e1279" TYPE="ext4"
/dev/mmcblk0: PTUUID="3fe6837a" PTTYPE="dos"





pi@pihumboldt:/mnt $ sudo blkid
/dev/mmcblk0p1: LABEL_FATBOOT="boot" LABEL="boot" UUID="7581-8A48" TYPE="vfat" PARTUUID="3fe6837a-01"
/dev/mmcblk0p2: LABEL="rootfs" UUID="fa37d505-e741-4d35-bcec-4580aef395e1" TYPE="ext4" PARTUUID="3fe6837a-02"
/dev/mmcblk0: PTUUID="3fe6837a" PTTYPE="dos"
/dev/sda1: PARTLABEL="os" PARTUUID="21908453-074c-477e-ba7c-d40817e06f71"
/dev/sda2: LABEL="data-ntfs" UUID="343D955A0BBBC2CB" TYPE="ntfs" PTTYPE="dos" PARTLABEL="data-ntfs" PARTUUID="4d61f4ec-85ca-417a-b178-b1f2e9965b39"
/dev/sda3: LABEL="data-ext4" UUID="dab405d8-c03d-4819-8b8b-125d89430431" TYPE="ext4" PARTLABEL="data-ext4" PARTUUID="a897cb81-7a1b-4ae1-bd94-390a83d0bef0"

pi@pihumboldt:~ $ sudo blkid
/dev/mmcblk0p1: LABEL_FATBOOT="boot" LABEL="boot" UUID="7581-8A48" TYPE="vfat" PARTUUID="3fe6837a-01"
/dev/mmcblk0p2: LABEL="rootfs" UUID="fa37d505-e741-4d35-bcec-4580aef395e1" TYPE="ext4" PARTUUID="3fe6837a-02"
/dev/mmcblk0: PTUUID="3fe6837a" PTTYPE="dos"
/dev/sda1: LABEL="rootfs" UUID="fa37d505-e741-4d35-bcec-4580aef395e1" TYPE="ext4" PARTLABEL="os" PARTUUID="21908453-074c-477e-ba7c-d40817e06f71"
/dev/sda2: LABEL="data-ntfs" UUID="343D955A0BBBC2CB" TYPE="ntfs" PTTYPE="dos" PARTLABEL="data-ntfs" PARTUUID="4d61f4ec-85ca-417a-b178-b1f2e9965b39"
/dev/sda3: LABEL="data-ext4" UUID="dab405d8-c03d-4819-8b8b-125d89430431" TYPE="ext4" PARTLABEL="data-ext4" PARTUUID="a897cb81-7a1b-4ae1-bd94-390a83d0bef0"
pi@pihumboldt:~ $ 