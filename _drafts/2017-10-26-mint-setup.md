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

Well Cinnamon is quite different and I thought it could be something like Gnome but looks like it used to be a fork from Gnome and then turned into its own DE. 

Cinnamon has intergrated most of the basic functions to control the appearance of the desktop environment and provided some of the applets to be used. So far I haven't found any that's really interesting to me. (guess I'm just picky). But one thing I do miss from GNOME 3 is the ShellTile extension that groups windows all together and being able to resize, move, act lik a family. Maybe Cinnamon also has that but it remains to be found out.

#### Vim Fuzzy Finder
Definitely a life saver. Recommended without another thought. Has to be there on all my Linux setup. 

Check it out from [FuzzyFinder's Github Repo](https://github.com/vim-scripts/FuzzyFinder)

The setup should be fairly easy under Linux, just unzip and copy to home directory with ```.vimsrc``` file. Here I logged the way to set it up under Windows 10 Bash on Ubuntu on Windows with Cmder.

The directory to put the folders is under ```C:\Users\[Windows_User]\AppData\Local\lxss\home\[Linux_User]```

I had a hard time finding the directory under my machine I don't know why, but with the help of [Everything](https://www.voidtools.com/){:target="_blank"} it's much easier to locate almost any file in your machine. 

#### Chinese Character Fonts Setting
Turns out the support for Chinese character is not perfect under Linux Mint. One font I found quite eyecandy is [Overpass](http://overpassfont.org/), an open source project. There are a couple of extra settings to bypass the fonts set by the system or the theme.

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
