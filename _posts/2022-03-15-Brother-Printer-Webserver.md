---
bg: "tools.jpg"
layout: post
title:  Webserver for a Brother QL-500 Printer
crawlertitle: Webserver Brother Printer
summary: Webserver for a Brother QL-500 Printer
date:   2022-03-15
categories: posts
tags: ['labdoo','linux','python']
author: jfdzar
---

For the Labdoo project I have to print the device tags and stick them to the laptops.
At the beginning I was printing them in normal paper and then putting tape on them.
The process was horrible and I lose a lot of time, until I saw this post in our Coffe Wall [Labels](https://platform.labdoo.org/de/content/labels).</br>

I decided to investigate a bit and I discover that there was a guy who grote a python library for the QL Brother Printers [Brother QL on Github](https://github.com/pklaus/brother_ql). So I though, I have to make this work!

And I created a python program which created a webserver with flask to print the labels from Labdoo and much other things [BrotherPrinterWebServer](https://github.com/jfdzar/BrotherPrinterWebServer). I created a more simple program without webserver in case someone is intereset [Brother QL Labdoo Tags Printer](https://github.com/jfdzar/brother_ql_labdoo_tags_printer).

The installation process is well documented in the repository [BrotherPrinterWebServer](https://github.com/jfdzar/BrotherPrinterWebServer). So I won't be repeating everything but I wanted to give a bit of a Background here!

