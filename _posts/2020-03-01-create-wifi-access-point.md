---
bg: "tools.jpg"
layout: post
title:  Create a Wifi Access Point
crawlertitle: Create a Wifi Access Point
summary: Create a Wifi Access Point
date:   2020-03-01
categories: posts
tags: ['raspberry', 'linux']
author: jfdzar
---

Source: https://thepi.io/how-to-use-your-raspberry-pi-as-a-wireless-access-point/

* First install hostapd and dnsmasq
```bash
sudo apt-get install hostapd
sudo apt-get install dnsmasq
```
* Stop both services
{% highlight bash %}
sudo systemctl stop hostapd
sudo systemctl stop dnsmasq
{% endhighlight %}

* Configure Statis IP for Wlan0 interface
```bash
sudo nano /etc/dhcpcd.conf
```
* Write the following at the end of the file
```bash
interface wlan0
static ip_address=192.168.0.10/24
denyinterfaces eth0
denyinterfaces wlan0
```
* Configure DHCP Server
```bash
sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
sudo nano /etc/dnsmasq.conf
```
* Write the following in the file
```bash
interface=wlan0
  dhcp-range=192.168.0.11,192.168.0.30,255.255.255.0,24h
```
* Configure the access point host software (hostapd)
```bash
sudo nano /etc/hostapd/hostapd.conf
```
* Write the following in the file
```bash
interface=wlan0
hw_mode=g
channel=7
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
ssid=NETWORK
wpa_passphrase=PASSWORD
```
* Show the system the location of the file
```bash
sudo nano /etc/default/hostapd
```
* Write the following to the file
```bash
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```


* I had problems starting the services hostapd and I follow the instructions of this link running the following commands it worked… I also run something of the ip_tables but I do not know if it was related.
```bash
sudo systemctl unmask hostapd
sudo systemctl enable hostapd
sudo systemctl start hostapd
```