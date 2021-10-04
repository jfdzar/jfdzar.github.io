---
bg: "tools.jpg"
layout: post
title:  Installing Numpy and Pandas in Raspberry Pi
crawlertitle: Installing Numpy and Pandas in Raspberry Pi
summary: Installing Numpy and Pandas in Raspberry Pi
date:   2020-03-08
categories: posts
tags: ['raspberry','linux','python']
author: jfdzar
---

It looks like installing numpy and pandas in the raspberry is not as straight forward as we though...
I think this problem was already solved...

Getting the answer from here: [link](https://stackoverflow.com/questions/53784520/numpy-import-error-python3-on-raspberry-pi)

Moving my comment to an answer because it seemed helpful to a few users.
You are missing a core numpy dependency. Running the following command should fix the problem.

```bash
sudo apt-get install python-dev libatlas-base-dev
```

If that doesn't work, you can try installing RPi specific versions of numpy, see comments here.

Executing that command made numpy work on my Rpi without problems

Good thing of this topic is that I got some insides on virutal enviroments! which are coool!

[See Youtube Video](https://www.youtube.com/watch?v=N5vscPTWKOk)


