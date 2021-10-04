---
bg: "tools.jpg"
layout: post
title:  Installing missing dependencies python library in raspberry
crawlertitle: Installing missing dependencies python library in raspberry
summary: Installing missing dependencies python library in raspberry
date:   2020-03-11
categories: posts
tags: ['raspberry','linux','python']
author: jfdzar
---

Installing opencv in raspberry pi was a bit tricky
When importing I got the error

```python
ImportError: libhdf5_serial.so.103: cannot open shared object file: No such file or directory
```

To solve this I was looking for stackoverflow answers but the best way was described here
[Source Link](https://blog.piwheels.org/how-to-work-out-the-missing-dependencies-for-a-python-package/)


I will make a copy paste in case the article gets deleted:

27 September 2018
## How to work out the missing dependencies for a Python package
When you install a compiled Python wheel, whether it’s from PyPI or piwheels, it will likely depend on some shared libraries, specifically certain .so files (shared object files) in order to be used.

If you’ve ever been in the situation where you’ve installed a library but importing it fails, it’s a pretty unpleasant experience:

[![Screenshot01]({{ site.images | relative_url }}/python-dependencies-01.png)]({{ site.images | relative_url }}/python-dependencies-01.png)

The next step for most people is to Google the error message. But that’s a long and slow process that often doesn’t lead to a successful import.

The best way to resolve this issue requires a couple of command line tools: ldd and apt-file.

First, navigate to the location of the package installation. This is usually /usr/local/lib/python3.5/dist-packages/<package>/. Note the package directory will be named after the import line, which may differ from the name of the package as you installed it. For example, you pip install numpy and import numpy but you pip install opencv-python and import cv2.

Run ls in that directory and look for an .so file:

```bash
pi@raspberrypi:/usr/local/lib/python3.5/dist-packages/cv2 $ ls
cv2.cpython-35m-arm-linux-gnueabihf.so data __init__.py __pycache__
```

Run ldd on that file:

```bash
ldd cv2.cpython-35m-arm-linux-gnueabihf.so
```
(tab completion is your friend)

You’ll see a lot of .so files. Those are shared objects the Python library source code refers to. Some of them will be available on your system, and will show the location they can be found:

```bash
libpthread.so.0 => /lib/arm-linux-gnueabihf/libpthread.so.0 (0x74fdb000)
```

Others will show “not found”. These are the ones you need to make available:

```bash
libhdf5_serial.so.100 => not found
```

You can use grep to filter out the found ones:

```bash
ldd cv2.cpython-35m-arm-linux-gnueabihf.so | grep "not found"
```

To find out which apt packages provide this .so, use apt-file. apt-file isn’t installed by default, so install it with apt:

```bash
sudo apt install apt-file
```

You’ll want to update apt-file‘s cache:

```bash
sudo apt-file update
```

Then use apt-file search on the missing .so file:

```bash
apt-file search libhdf5_serial.so.100
```

This will show a list of apt packages (including some duplicates):

```bash
libhdf5-100: /usr/lib/arm-linux-gnueabihf/libhdf5_serial.so.100
libhdf5-100: /usr/lib/arm-linux-gnueabihf/libhdf5_serial.so.100.0.1
```

This indicates that the package libhdf5 will provide the required .so file opencv refers to. So install it:

```bash
sudo apt install libhdf5-100
```

That’s it! Just rinse and repeat. Once you’ve made all the missing shared object files available, you’ll be able to import the module no problem:

[![Screenshot02]({{ site.images | relative_url }}/python-dependencies-02.png)]({{ site.images | relative_url }}/python-dependencies-02.png)

Note that some shared objects can be provided by multiple packages. Sometimes it’s obvious which is the lighter option, i.e. libatlas3-base rather than libatlas-base-dev (avoid -dev packages if possible), or libpango-1.0-0 rather than the humongous wolfram-engine. You can see the file size with apt-cache show:

```bash
pi@raspberrypi:~ $ apt-file search libpango-1.0.so.0
libpango-1.0-0: /usr/lib/arm-linux-gnueabihf/libpango-1.0.so.0
libpango-1.0-0: /usr/lib/arm-linux-gnueabihf/libpango-1.0.so.0.4000.5
wolfram-engine: /opt/Wolfram/WolframEngine/11.3/SystemFiles/Libraries/Linux-ARM/libpango-1.0.so.0
pi@raspberrypi:~ $ apt show libpango-1.0 | grep Size

Installed-Size: 515 kB
Download-Size: 305 kB
pi@raspberrypi:~ $ apt show wolfram-engine | grep Size

Installed-Size: 829 MB
Download-Size: 306 MB
```

As you can see, the choice here is an easy one: 300 kB vs 300MB!

We’re planning to add project pages to piwheels.org, which will feature library dependencies so you don’t have to look them up manually. If you were looking for opencv requirements, see our blog post [New opencv builds](https://blog.piwheels.org/new-opencv-builds/) which includes the lists of dependencies for the opencv packages.