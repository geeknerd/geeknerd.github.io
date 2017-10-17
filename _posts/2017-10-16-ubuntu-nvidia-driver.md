---
layout: post
title: Install NVIDIA Driver on Ubuntu 17.04 for GTX1050Ti Graphic Card
excerpt: "Basically a way to install the latest NVIDIA driver for GTX1050Ti card on a laptop in Ubuntu."
date: 2017-10-16
comments: true
pinned: true
tags: [Linux, Ubuntu]
image:
  feature: ubuntu.jpg
  credit: 
  creditlink: 
---

Although Ubuntu has integrated drivers for most devices, some of the new graphic cards still need specific driver from their providers to work normally on Ubuntu system. My GTX1050Ti is one of those cards and here is a solution to make Linux on my Windows machine posible. Honestly, this is a combination of several solutions to make things happen. 

<!--more-->

## Hardware configuration:
HP Omen 15 Laptop  
CPU: Core i5-7730HQ  
Graphics: NVIDIA GTX1050Ti

## Issue encountered:
Windows 10 is good, with the new Ubuntu bash integration, it's almost packed for developers and should satify most people. Yet, working in a Linux environment is more doable for back-end developers and no gaming is what I really seek (Battlegrounds is killing me really). Anyway, I tried to install Ubuntu 17.04 to the SSD that I have on Omen but no matter what option I choose or how I partition the driver, it just didn't work out. Sometimes it freezes after installation complete on restart page, sometimes it freezes after restart on login page, sometimes it finally gets into the desktop and freezes after I click on the settings button. :smirk: 

At first I thought it could be issues with the ISO I used for Ubuntu or the USB drive I used to install, so I tried different ones and no results. After endless searching online I realized the problem could be due to my graphic card driver. (Well I actually thought it's fine when I see the correct resolution during installation). Solutions follow.

## Solutions:
### Disable *nouveau* driver
Ubuntu uses nouveau as its graphic card driver, which we need to disable from the kernel in order to install NVIDIA official driver. Adding nouveau to blacklist.conf file will preventing linux from loading nouveau on startup.  
Due to the nouveau driver, Ubuntu can't log into desktop, thus no terminal to use. Therefore, at the login page, enter TTY mode by pressing ```Ctrl+Alt+F1```.

Remember to change permission for blacklist.conf first then revert it back. 
```shell
ll /etc/modprobe.d/blacklist.conf
```

Set permission
```bash
sudo chmod 666 /etc/modprobe.d/blacklist.conf
```

Edit it with your favorite editor:
~~~bash
sudo vi /etc/modprobe.d/blacklist.conf
~~~

Append these to the end of the file  

blacklist vga16fb  
blacklist nouveau  
blacklist rivafb  
blacklist rivatv  
blacklist nvidiafb  
{: .notice}

Revert back the permission for safety.
```bash
sudo chmod 644 /etc/modprobe.d/blacklist.conf
```

Remember to update the kernel before use.
```bash
sudo update-initramfs -u
```

**Remember to reboot at this point.** 

Make sure nouveau is blacklisted. 
```bash
lsmod | grep nouveau
```

### Install NVIDIA driver
Unless the hardware doesn't come with a integrated graphic card, at this point, it should be possible to enter Ubuntu desktop environment. (Mixed resolution might apply but don't pacnic... yet). Now we add official driver through Terminal. 
```bash
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
```
Remember to search for your suitable (recommended) driver version. 
```bash
ubuntu-drivers devices
```
![]({{site.url}}/img/device.png)
{: .center}
*If the recommended version doesn't work, try different ones.*  

At this point, remember the version name, ```nvidia-378``` in this case.  
Enter TTY mode by ```Ctrl+Alt+F1``` to close display manager LightDM
~~~ shell
sudo service lightdm stop
~~~
Now, install the NVIDIA driver and reboot.  
Might take a while depending on the network speed. 
~~~ shell
sudo apt-get install nvidia-378
sudo reboot
~~~
Hopefully, everything works out and login works fine.  
Check if driver installed correctly and settings could be used.
~~~ shell
sudo nvidia-smi
sudo nvidia-setting
~~~
*Pictures see the top.*

### BIOS Setting
Remember to set Secure Boot to Disabled in BIOS settings when installing NVIDIA driver. Otherwise errors might occur. 

Everything should be good to go.