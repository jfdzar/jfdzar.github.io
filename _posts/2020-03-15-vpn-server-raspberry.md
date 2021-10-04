---
bg: "tools.jpg"
layout: post
title:  VPN Server with Raspberry Pi PiVPN and IPV6
crawlertitle: VPN Server with Raspberry Pi PiVPN and IPV6
summary: VPN Server with Raspberry Pi PiVPN and IPV6
date:   2020-03-15
categories: posts
tags: ['raspberry','linux']
author: jfdzar
---

After looking a lot how to create a VPN Server for my home I accidentally found this great tutorial in german: [link](https://blog.helmutkarger.de/raspberry-pi-vpn-teil-6-vpn-server-unter-ipv6/)

Everything worked fine as explained in the tutorial
I also add FritzBox router so it was even easier for my with the myfritz possibilities.

The only think it didn't work is that when connected through the VPN the client was not able to access internet and local network. 
I discovered somehow the ip tables were not right so I followed that part of this tutorial and everything worked perfect [link](https://2ellsblog.wordpress.com/2016/02/09/osmc-pi-openvpn-server-set-up-openvpn-server/)

Note, this is where the set up for OpenVPN on OSMC differs from Raspian.

In the terminal window type the following command; note, for the iptables command the IP address at the end of the command should be your Pi IP address (if you have logged in again since the last task then type sudo su first):

```bash
iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j SNAT --to-source 192.168.1.68;
```

Test this has worked by typing the command:

```bash
iptables -t nat -v -L
```

Next type the command (was already installed)
```bash
apt-get install iptables-persistent
```

and

```bash
iptables-save > /etc/iptables/rules.v4
cat /etc/iptables/rules.v4
```