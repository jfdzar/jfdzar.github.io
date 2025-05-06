---
bg: "tools.jpg"
layout: post
title:  Starting with MQTT
crawlertitle: Starting with MQTT
summary: Starting with MQTT with Arduino and Raspberry Pi
date:   2020-03-02
categories: posts
tags: ['raspberry', 'arduino','homeassistant']
author: jfdzar
---

General Links
Wemos d1_Mini https://wiki.wemos.cc/products:d1:d1_mini
MQTT ESP8266 and Raspberry Pi https://www.hackster.io/ruchir1674/raspberry-pi-talking-to-esp8266-using-mqtt-ed9037
Connect Raspberry Pi to ESP8266 https://openhomeautomation.net/connect-esp8266-raspberry-pi
Websocket Communication ESP8266 and Raspberry Pi https://diyprojects.io/websocket-communication-esp8266-arduino-python-test-ws4py-library-raspberry-pi/#.XEtdhFVKipr
SIM808 GPRS and GPS Tutorial: Not directly related with this project but could be useful https://www.prometec.net/sim808/https://www.prometec.net/gprs-llamar-enviar-sms/
Arduino MEGA Overview https://www.arrow.com/en/research-and-events/articles/arduino-mega-2560-overview
ADAFruit Motor Shield https://playground.arduino.cc/Main/AdafruitMotorShield

First Commands with MQTT
From the raspberry pi to listen to topic: test
mosquitto_sub -d -u username -P password -t test
mosquitto_sub -d -u elisensor -P Eli14Sens -t elisensor/feeds/mega
From the raspberry pi to publish on topic test
mosquitto_pub -d -u username -P password -t test -m "Hello, World!"
mosquitto_pub -d -u elisensor -P Eli14Sens -t elisensor/feeds/onoff -m “ON”
IMPORTANT: Arduino generates the topics name like username/xxx/xxx
Check the Adafruit example mqtt_esp8266
sudo systemctl stop mosquitto.service