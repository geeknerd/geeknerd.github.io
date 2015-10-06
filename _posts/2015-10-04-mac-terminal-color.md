---
layout: post
title: Customize Terminal Colors in El Capitan
date: 2015-10-04
comments: true
pinned: true
tags: [Mac OS X]
---

One of the most powerful tools on a Mac system would be the Terminal (or the trackpad as somebody insists). While most users won't even touch the Terminal on a daily basis, it stills has its value to most programmers or SE's or whoever wants to mess around with GNU. Among the Terminal users, part of them use the default settings that come with the system for Terminal, others would like to add their own colors to the app, to the latter I consider myself belong to. 
Now, to customize the colors in Terminal, essentially I'm assuming you want to see colorful ```ls``` and intuitive ```Vim```. And I also assume you're not planning on a customized background for your Terminal, which should somewhat look like this:
{: .center}
![Customized Background]({{size.url}}/img/terminal-theme-mac-os-x.jpg =300x)
//{: style="img-align: center"}

One simplest way to colorize Terminal would be using the ```-G``` argument that comes with ```ls```. To accomplish this, one could open up ```.bash_profile``` and add the following to it:
{% highlight bash %}
export CLICOLOR=1
export LSCOLORS=ExFxBxDxCxegedabagacad
alias ls='ls -GFh'
{% endhighlight %}
That should at least give you some colorful ```ls``` results. However, it doesn't give you the full power of controlling the colors in your Terminal and we all know that programmers want to take over everything as they can. So, a great GNU tool comes to the stage: [GNU Coreutils](http://www.gnu.org/software/coreutils/coreutils.html). Coreutils gives you the flexibility of controlling the colors but also other manipuation utilities you need from a GNU os. 
To get Coreutils, the easiest way is through ```Homebrew```:
{% highlight bash %}
brew install xz coreutils
{% endhighlight %}
Then you need to generate the color profile:
{% highlight bash %}
gdircolors --print-database > ~/.dir_colors
{% endhighlight %}
The last thing is to add the configuration into ```~/.bash_profile```
{% highlight bash %}
if brew list | grep coreutils > /dev/null ; then
  PATH="$(brew --prefix coreutils)/libexec/gnubin:$PATH"
  alias ls='ls -F --show-control-chars --color=auto'
  eval `gdircolors -b $HOME/.dir_colors`
fi
{% endhighlight %}
You could modify the colors in ```~/.dir_colors``` to match your personal preferences. But one additional thing is that you want to add the ```grep``` highlighting to your ```~/.bash_profile``` for your convenience. 
{% highlight bash %}
alias grep='grep --color'
alias egrep='egrep --color'
alias fgrep='fgrep --color'
{% endhighlight %}
Next, jumping to Vim, it will be much easier, just edit ```~/.vimrc``` and add:
{% highlight bash %}
syntax on
{% endhighlight %}
Of course, as a user who relies on ```Vim``` a lot, not me, you would also want something like: 
{% highlight bash %}
set tabstop=4
set softtabstop=4
set ts=4
set expandtab
set autoindent
set nu
{% endhighlight %}
There you go. Colorful Terminal! Wonderful life!
