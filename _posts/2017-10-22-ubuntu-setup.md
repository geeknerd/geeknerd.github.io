---
layout: post
title: Ubuntu 17.xx - Kernel, Network, GNOME and more
date: 2017-10-22
comments: true
pinned: true
tags: [Linux]
---

As unstable as Ubuntu is running on my major work machine, endless testing and re-installation is inevitable. Although I've been seeing a lot of comments about the trend of Linux development as well as how popular Fedora is going to be, my need for a Linux environment is merely a usable Terminal and some Linux packages. Windows 10 already has its Ubuntu Bash integration that could do most of my work but hey, a developer who doesn't mess around with his/her computer is not a well trained one. 

And of course, headaches come all the way even before I started to set it up. Anyway, I decided to search my way through obstacles and here logs the softwares I installed and the settings I set. No orders of importance, just ordered by my memory. 

<!--more-->

### First Things Tirst
Install the NVIDIA driver for Ubuntu 17.10.  
Well I've tested on 16.04LTS to 17.10. All worked the same way. See [This post]({{site.url}}{% post_url 2017-10-16-ubuntu-nvidia-driver %}).

Also, remember to do update and upgrade before installing more softwares and also periodically after some softwares are installed. 
``` shell
sudo apt-get update && sudo apt-get upgrade
```

### Changing Kernel
I'm not sure if this should be done before any other steps but the kernel 4.13 doesn't have support for my RTL8822BE wireless card. Therefore I have to downgrade it to 4.10 or earlier.

After goolging around for various solutions, there appears to be a simple solution to all these - using ukuu. 
``` shell 
sudo add-apt-repository -y ppa:teejee2008/ppa
sudo apt update
sudo apt install ukuu
```
After installation, open ukuu, refresh, select a kernel then install. After that restart and choose the corresponding kernel at Grub menu. 

Also, after rebooting, it's safe to remove the previous kernel either through ukuu or command line.
``` shell
sudo apt remove linux-headers-4.10* linux-image-4.10*
```

### Scientific Networking
Well, I hope this is self-explanatory. Shadowsocks seems to be one of the nice ways to get VPN connections overseas. So far the performance is good. 
``` shell
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install -y shadowsocks-qt5
```
Including one online PAC to use:
``` shell  
https://raw.githubusercontent.com/KyonLi/ss-pac/master/ss.pac 
```

### Sublime Text 3
Install the GPG key:
``` shell
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```
Ensure apt is set up to work with https sources: 
``` shell
sudo apt-get install apt-transport-https
```
Select the channel to use:  
**Stable**
``` shell
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
```
Update apt sources and install Sublime Text 
``` shell
sudo apt-get update
sudo apt-get install sublime-text
```

### Downloader Tools
uget + aria2 I personally is by far the fastest combination. There might be others but I prefer these. In uget, right click *All Category* and *Properties*, set *Default for new download 1* to Max Connections 16. 
``` shell
sudo apt-get install uget aria2
```
Then add chrome extension wrapper
{% highlight shell linenos %}
wget https://raw.githubusercontent.com/slgobinath/uget-chrome-wrapper/master/build/linux/install_uget_chrome_wrapper.sh
sudo sh install_uget_chrome_wrapper.sh
{% endhighlight %}

### Customization Tools
**Install GNOME Shell extensions & GNOME Tweak Tools:**
``` shell
sudo apt-get install gnome-shell-extensions gnome-tweak-tool
```
[Find Themes Here](https://www.gnome-look.org/)

**Default GNOME will mess up some themes, so recommended to install Vanilla GNOME.**
``` shell
sudo apt install gnome-session
```
[See here](http://www.omgubuntu.co.uk/2017/10/install-vanilla-gnome-shell-ubuntu-17-10)

**Extensions for GNOME tweak**

All the extensions can be now found [here](https://extensions.gnome.org/). 
