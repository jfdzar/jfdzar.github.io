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

### Printing Labdoo Tags with a Brother QL Printer

As part of the [Labdoo project](https://platform.labdoo.org/de/content/labels), I need to print and attach device tags to laptops. Initially, I was printing them on regular paper and covering them with tape — a frustrating and time-consuming process.

One day, I came across this [post on our Coffee Wall](https://platform.labdoo.org/de/content/labels) about printing proper labels, and it changed everything.

After a bit of research, I discovered a Python library made for Brother QL printers: [Brother QL on GitHub](https://github.com/pklaus/brother_ql). I thought: _I have to make this work!_

So, I created a Python tool that runs a small webserver using Flask to print Labdoo labels — and potentially much more:  
👉 [BrotherPrinterWebServer](https://github.com/jfdzar/BrotherPrinterWebServer)

For those who prefer simplicity or don’t want to run a webserver, I also made a lightweight version:  
👉 [Brother QL Labdoo Tags Printer](https://github.com/jfdzar/brother_ql_labdoo_tags_printer)

The installation is well documented in the repo, so I won’t repeat it all here. But I wanted to provide some background and share how this small improvement saved me a lot of time and hassle.

Also worth noting — I’ve recently added Docker support to the main project to simplify setup and improve reproducibility.

Happy printing!