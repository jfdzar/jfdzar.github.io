---
bg: "tools.jpg"
layout: post
title:  Installing HomeAssistant from Zero
crawlertitle: Installing HomeAssistant from Zero
summary: Installing HomeAssistant from Zero
date:   2020-03-16
categories: posts
tags: ['homeassistant','raspberry']
author: jfdzar
---

 I will document the process of installing HomeAssistant Raspberry Pi from the zero

1. Burn Raspbian Lite OS on the SD Card

2. Create "ssh" empty file on boot partition to be able to access ssh

3. Connect to Raspberry and change host name and password
```bash
sudo nano /etc/hosts
sudo nano /etc/hostname
passwd
```

4. Reboot and connect again

5. Run main configuration - set location, time zone, etc
```bash
sudo raspi-config
sudo apt-get update and sudo apt-get upgrade
```

6. Install Docker - following [this guide](https://phoenixnap.com/kb/docker-on-raspberry-pi)

7. Install Home Assistant - [following official guide platform install](https://www.home-assistant.io/installation/raspberrypi)
docker compose also explained here

9. Run Home Assistant with Docker Compose (actually not sure if step with Mosquitto MQTT needed)
https://iotechonline.com/home-assistant-install-with-docker-compose/
https://chrisschuld.com/2019/09/running-home-assistant-with-docker/

10. Configure Access Point WLAN - [following my guide](/posts/create-wifi-access-point)

11. Install Mosquitto MQTT and configure password- [following this guide](https://iot4beginners.com/mosquitto-mqtt-broker-on-raspberry-pi/)

12. Configure Samba following [this guide](https://magpi.raspberrypi.org/articles/samba-file-server) 

After that system should be ready to run!

Add the optional scripts you like


# Other Guides that were useful
* [Running Home Assistant with Docker](https://chrisschuld.com/2019/09/running-home-assistant-with-docker/)
* [HA Install with Docker Compose](https://iotechonline.com/home-assistant-install-with-docker-compose/)

Backup was solve in another way with a script - to be versioned
* [Backup Docker Base Home Assistant to AWS](https://chrisschuld.com/2019/09/backup-docker-based-home-assistant-to-s3/)

Another interesting article about the topic
* [HA Panel iframe with external access](https://iotechonline.com/home-assistant-panel_iframe-external-access-with-nginx-proxy/)


