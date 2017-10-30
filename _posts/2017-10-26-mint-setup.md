---
layout: post
title: The way I setup my Linux (Linux Mint)
date: 2017-10-26
comments: true
pinned: true
tags: [Linux]
---

As famous as it's own reputation, Ubuntu's "Internal Error Occured" is really driving me crazy lately and I decided to take a look into a more novice-friendly linux distro - Linux Mint, ranked No.1 in Distro Watch. Apprently, I should've checked this out earlier in my life before all the headache. 

Anyway, here are some of the tips during the usage of Linux Mint. Including but not limited to some of the useful softwares for Linux I found worth recommending. 

<!--more-->
For some of the basic setup, it's doable to refer to the setup of Ubuntu since Linux Mint is based on that. 

Well, Cinnamon is quite different and I thought it could be something like Gnome but looks like it used to be a fork from Gnome and then turned into its own DE. 

Cinnamon has intergrated most of the basic functions to control the appearance of the desktop environment and provided some of the applets to be used. So far I haven't found any that's really interesting to me. (guess I'm just picky). But one thing I do miss from GNOME 3 is the ShellTile extension that groups windows all together and being able to resize, move, act lik a family. Maybe Cinnamon also has that but it remains to be found out.

*Update*  
Cinnamon has the *snap* Windows function that basically reserves a place for one window and maximize the other to the rest. :confused: Not what I prefer but works great. 

#### First Things First - The Graphics Driver
Ironically, I don't even need to configure the graphic driver anymore. I guess that's the beauty of Linux Mint's hardware compatibility.

***UPDATE***

After upgrading the kernel from 4.8 to 4.10, the magic of nouveau on Linux Mint doesn't hold anymore.:flushed: Therefore, I assume the problem is not with Ubuntu itself but with kernels newer than 4.8. Anyway, just go through the NVIDIA driver installation again should solve the problem. 

#### Install Network Adapter RTL8822be Driver
[Update Kernel If Necessory]({{site.url}}{% post_url 2017-10-22-ubuntu-setup %}), kernel 4.13 yields compilation errors so use 4.10 or blew for now. Then: 
{% highlight shell linenos %}
sudo apt update
sudo apt install git
git clone https://github.com/rtlwifi-linux/rtlwifi-next
cd rtlwifi-next
make
sudo make install
sudo modprobe rtl8822be
{% endhighlight %}

#### DNS Settings For apt-get update
One problem I encountered was that apt-get update always failed to fetch packages whenever a new PPA was added. Even I tried to set global proxy or just terminal proxy, most of the times it doesn't work. Looks like for now getting some good entries for DNS server alternatives is a good solution for this. Here is how:  

Edit file ```/etc/resolv.conf``` and add public DNS of faster speed. Google, Aliyun, or others. 
``` shell
nameserver 127.0.1.1
nameserver 8.8.8.8
nameserver 8.8.4.4  
nameserver 114.114.114.114
nameserver 114.114.115.115
nameserver 223.5.5.5
nameserver 223.6.6.6
```
Or add those to base file under ```/etc/resolvconf/resolv.conf.d```. 

Restart service 
``` shell
sudo /etc/init.d/resolvconf restart
```

Alternatively, I've tried to set global proxy in Terminal by :
``` shell
export ALL_PROXY=socks5://127.0.0.1:1080
```
Sometimes works, sometimes doesn't. 

#### Terminal Setting
Gnome Terminal is good enough, but I like Zsh themes better.

Therefore, install Zsh, then install oh my zsh, then customize as you like .

{% highlight shell linenos%}
sudo apt-get install zsh
# curl
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
# wget
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

# ZSH_THEME=agnoster
# agnoster requires powerline fonts
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts

# Color Scheme is Ocean Dark from Gogh (Very Convenient)
sudo apt-get install dconf-cli
wget -O gogh https://git.io/vQgMr && chmod +x gogh && ./gogh && rm gogh
# choose 97
# or
# wget -O xt  https://git.io/vQ9TY && chmod +x xt && ./xt && rm xt
{% endhighlight %}

Quake - Not a must-have, but very handy terminal by one hotkey that drops from the top of the screen. 

Normally I let the local server run in Quake so I don't need to worry about it. 

Comes with distro library so should be able to install by simply ```sudo apt-get install quake -y```.

#### Vim Fuzzy Finder
Definitely a life saver. Recommended without another thought. Has to be there on all my Linux setup. 

Check it out from [FuzzyFinder's Github Repo](https://github.com/vim-scripts/FuzzyFinder)

The setup should be fairly easy under Linux, just unzip and copy to home directory with ```.vimsrc``` file. Here I logged the way to set it up under Windows 10 Bash on Ubuntu on Windows with Cmder.

The directory to put the folders is under ```C:\Users\[Windows_User]\AppData\Local\lxss\home\[Linux_User]```

I had a hard time finding the directory under my machine I don't know why, but with the help of [Everything](https://www.voidtools.com/){:target="_blank"}, it's much easier to locate almost any file on your machine. 

#### Chinese Character Fonts Setting
Turns out the support for Chinese character is not perfect under Linux Mint. One font I found quite eyecandy is [Overpass](http://overpassfont.org/){:target="_blank"}, an open source project. There are a couple of extra settings to bypass the fonts set by the system or the theme.

``` shell
sudo apt-get install language-selector-common
``` 
Make sure kate is installed then:
``` shell
sudo kate /var/lib/locales/supported.d/zh-hans
```
Add the following to fully support Chinese.
{% highlight shell linenos %}
{% raw %}
en_US.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8
zh_CN.GBK GBK
zh_CN GB2312
zh_CN.GB18030 GB1803
zh_HK BIG5-HKSCS
zh_HK.UTF-8 UTF-8
zh_SG GB2312
zh_SG.GBK GBK
zh_SG.UTF-8 UTF-8
zh_TW BIG5
zh_TW.EUC-TW EUC-TW
zh_TW.UTF-8 UTF-8
{% endraw %}
{% endhighlight %}

Then excute the following, reboot or not. 
``` shell
sudo locale-gen
```

#### Chinese Input Double Icons Removal
After installing SogouPinyin on Linux it shows two frames while typing, simply kill fcitx-qimpanel and add it to system startup to kill. 
``` shell
ps -ef | grep fcitx-qimpanel
sudo kill -9 [对应的pid]
sudo vim /etc/rc.local
# add before exit 0
/bin/ps -ef | grep fcitx-qimpanel | grep -v grep | awk '{print $2}' | xargs kill -9
```

#### Install VMware
Assuming you have the .bundle file downloaded.
``` shell
chmod a+x VMware-Workstation-Full-14.0.0-6661328.x86_64.bundle
sudo ./VMware-Workstation-Full-14.0.0-6661328.x86_64.bundle
```

#### Set Clock Time on Dual-Boot Systems
If you're dual-booting Linux Mint 18 and Windows 10, you may find that changing time in one system affects the other and the two systems can't display the same time.

This happens as Linux Mint 18 interprets the hardware clock or real time clock (RTC) in universal time (UTC) by default while Windows 10 maintains the clock in local time.

You can fix this by keeping RTC in local time in Linux Mint, same as Windows, by running a command in the terminal below.
``` shell
timedatectl set-local-rtc 1 --adjust-system-clock
```

Source: [Tips and Tricks for Linux Mint](https://www.techsupportalert.com/content/tips-and-tricks-linux-mint-after-installation-mint-18-cinnamon-edition.htm#Set-Clock-Time){:target="_blank"}


## Word of Advice
As an unprofessional programmer, I still couldn't live to the bar of file naming conventions. And prices are paid. :unamused:

**Never use space in file and folder name!!!** 