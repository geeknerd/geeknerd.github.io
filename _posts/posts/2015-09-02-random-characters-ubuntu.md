---
layout: post
title: Solving Random Characters in Ubuntu 14.04
date: 2015-09-02
modified: 2015-09-15
tags: [Linux]
comments: true
pinned: false
image: ubuntu.jpg
imageW: 200

---

After fresh install of Ubuntu 14.04, the default editor `gedit` will not show correct encodings for Chinese characters. And the old method does not work anymore in Ubuntu 14.04, or I was missing something from that. Buy anyway, an easy workaround would be to open terminal, enter the following command and restart gedit. Should also work on other encodings. 

{% highlight bash %}
gsettings set org.gnome.gedit.preferences.encodings auto-detected "['GB18030', 'GB2312', 'GBK', 'UTF-8', 'BIG5', 'CURRENT', 'UTF-16']"

gsettings set org.gnome.gedit.preferences.encodings shown-in-menu "['GB18030', 'GB2312', 'GBK', 'UTF-8', 'BIG5', 'CURRENT', 'UTF-16']"
{% endhighlight %}

To add encoding support to vim, which is one of the finest text editors you will be using in linux, add the following two lines to your `.vimrc` file. If you don't have one, create one at home directory should suffice. 
{% highlight bash %}
set fileencodings=utf-8,gb2312,gbk,gb18030,big5
set termencoding=utf-8,gb2312,gbk,gb18030
{% endhighlight %}
