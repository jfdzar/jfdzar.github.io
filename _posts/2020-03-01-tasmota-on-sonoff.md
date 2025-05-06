---
bg: "tools.jpg"
layout: post
title:  Tasmota on Sonoff
crawlertitle: Tasmota on Sonoff
summary: Tasmota on Sonoff
date:   2020-03-01
categories: posts
tags: ['homeassistant','arduino']
author: jfdzar
---

The main information about the proyect is here

Source: https://tasmota.github.io/docs/#/installation/Initial-Configuration

Last time I checked the project was very detailed to run everything


## Run Tasmotizer on Linux 
I run on the problem that I cannot install tasmotizer using normal pip. In order to make it run I used this trick (I do not remember where did I find the information to do that)

```bash
sudo apt-get install python3-venv
python3 -m venv vtas
cd vtas/
source bin/activate
pip install --upgrade pip setuptools pyserial --upgrade
pip install tasmotizer
cd /DirectoryWhereTasmotizer.py is located/
python3 tasmotizer.py 
```