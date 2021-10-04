---
bg: "tools.jpg"
layout: post
title:  Add Permisions to Printers udev rules
crawlertitle: Add Permisions to Printers udev rules
summary: Add Permisions to Printers udev rules
date:   2020-03-10
categories: posts
tags: ['linux']
author: jfdzar
---

Trying to make the script to automatically print the tags from labdoo I run into the problem that from python script I did not have permissions to access the printer.

We had similar problems when working with Platformio and the trying to program the boards.

Running the program in sudo will solve the problem, but does not a solution I want to use the whole time Making a small research I found the udev rules.
I tryied different soluions:
1. Add my user to the group lp - did not work
2. Creating a udev rule in /etc/udev/rules.d/10-local.rules with following line KERNEL=="lp0", SUBSYSTEM=="usb", MODE="0666" It did not work as well
3. At the end what worked was this tutorial Changing this file sudo nano /lib/udev/rules.d/50-udev-default.rules On the line lp is listed I added MODE="0666" And that worked 

[Link Solution 3 - Broken Link :(](https://askubuntu.com/questions/488182/how-to-create-persistent-symbolic-links-and-fix-permissions-to-use-the-raw-print https://unix.stackexchange.com/questions/95968/permissions-to-print-directly-to-usb-printer)