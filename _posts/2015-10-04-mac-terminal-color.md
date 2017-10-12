---
layout: post
title: Customize Terminal Colors in Mac OS X
date: 2017-08-29
comments: true
pinned: true
tags: [Mac OS X]
---

One of the most powerful tools on a Mac system would be the Terminal (or the trackpad as somebody insists). While most users won't even touch the Terminal on a daily basis, it stills has its value to most programmers or SE's or whoever wants to mess around with GNU. Among the Terminal users, part of them use the default settings that come with the system for Terminal, others would like to add their own colors to the app, to the latter I consider myself belong to. 
Now, to customize the colors in Terminal, essentially I'm assuming you want to see colorful ```ls``` and intuitive ```Vim```. And I also assume you're not planning on a customized background for your Terminal, which should somewhat look like this:

![]({{site.url}}/img/terminal-theme-mac-os-x.jpg){:height="700px" .center-image}


One simplest way to colorize Terminal would be using the ```-G``` argument that comes with ```ls```. To accomplish this, one could open up ```.bash_profile``` and add the following to it:

~~~ shell
export CLICOLOR=1
export LSCOLORS=ExFxBxDxCxegedabagacad
alias ls='ls -GFh'
~~~ 

That should at least give you some colorful ```ls``` results. However, it doesn't give you the full power of controlling the colors in your Terminal and we all know that programmers want to take over everything as they can. So, a great GNU tool comes to the stage: [GNU Coreutils](http://www.gnu.org/software/coreutils/coreutils.html). Coreutils gives you the flexibility of controlling the colors but also other manipuation utilities you need from a GNU os. 
To get Coreutils, the easiest way is through ```Homebrew```:

~~~ shell
brew install xz coreutils
~~~

Then you need to generate the color profile:

~~~ shell
gdircolors --print-database > ~/.dir_colors
~~~

The last thing is to add the configuration into ```~/.bash_profile```

~~~ shell
if brew list | grep coreutils > /dev/null ; then
  PATH="$(brew --prefix coreutils)/libexec/gnubin:$PATH"
  alias ls='ls -F --show-control-chars --color=auto'
  eval `gdircolors -b $HOME/.dir_colors`
fi
~~~

You could modify the colors in ```~/.dir_colors``` to match your personal preferences. But one additional thing is that you want to add the ```grep``` highlighting to your ```~/.bash_profile``` for your convenience. 

~~~ shell
alias grep='grep --color'
alias egrep='egrep --color'
alias fgrep='fgrep --color'
~~~

Next, jumping to Vim, it will be much easier, just edit ```~/.vimrc``` and add:

~~~ shell
syntax on
~~~

Of course, as a user who relies on ```Vim``` a lot, not me, you would also want something like: 

~~~ shell
set tabstop=4
set softtabstop=4
set ts=4
set expandtab
set autoindent
set nu
~~~

There you go. Colorful Terminal! Wonderful life!
(Mentioned methods have been tested on Yosemite and Sierra, not guaranteed to work on all versions.)
