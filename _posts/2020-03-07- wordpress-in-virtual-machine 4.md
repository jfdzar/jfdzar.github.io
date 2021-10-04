---
bg: "tools.jpg"
layout: post
title:  Installing Wordpress in a Virtual Machine for local test
crawlertitle: Installing Wordpress in a Virtual Machine for local test
summary: Installing Wordpress in a Virtual Machine for local test
date:   2020-03-07
categories: posts
tags: ['linux','wordpress']
author: jfdzar
---

This was not as easy as I expected at the beginning...

## Install Ubuntu Server on a Virtual Box Machine
First of all I download an install Virtual Box on my machine following this tutoria: [Link](https://hibbard.eu/install-ubuntu-virtual-box/)

nice and easy it explains you also how to configure virtual box to access the server through ssh on you local network -> Very helpfull

## Install Wordpress on Ubuntu Server
After doing that I install wordpress on the ubuntu server following "partially" this tutorial: [Link](https://ubuntu.com/tutorials/install-and-configure-wordpress#1-overview)

At some point I changed the "localhost" to the ip-address I had assigned to my ubuntu server because I was accessing the server from the local network, not from the machine itself.

Here I do not know if I did the correct solution, but somehow worked

## Solving Issue installing themes
I had a problem installing a theme

First because Wordpress asked for the ftp credentials I solved it with the recomendations of this website: [Link](https://www.garron.me/en/bits/wordpress-plugin-and-theme-install-without-ftp-credentials.html)
As simple as adding this line

```php
define('FS_METHOD', 'direct');
```

to the config file

/usr/share/wordpress/wp-config.php

Second I had access problems when the theme was installing to create the needed directories. It was a permissions issue and I solved it with this command:

```bash
sudo chown -R www-data:www-data /usr/share/wordpress/wp-content/
```

After that server was up and running with a test Wordpress Instance