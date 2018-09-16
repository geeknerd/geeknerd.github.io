---
layout: post
title: Bash Commands for Better Productivity
date: 2018-09-15
modifited: 2018-09-15
comments: true
pinned: true
tags: [Linux]
---
##### Count number of files or directories under a certain directory. 
This will list all non-hidden entries and extract out directories and do a count on them. 
{% highlight shell %}
ls -l | grep "^d" | wc -l
{% endhighlight %}

Or use a simpler version:
{% highlight shell %}
ls -l | grep -c ^d
ls -l | grep -c ^- #this counts the files without directories
{% endhighlight %}

There is another way using ```echo``` command.
{% highlight shell %}
echo */ | wc
{% endhighlight %}

To search for empty folders in a specific directory, use the ```find``` command with arguments like:
{% highlight shell %}
find . -type d -empty
{% endhighlight %}

To list all the directories under a certain directory:
{% highlight shell %}
ls -d */
{% endhighlight %}

To find all non-empty directory under the current directory, excluding the parent ```.```
{% highlight shell %}
find . -mindepth 1 -type d -not -empty -printf '%P\n' | sort
{% endhighlight %}

To find files with certain sizes (larger/smaller than)
{% highlight shell %}
find . -maxdepth 1 -type f -name "*.csv" -size -11M  # +11M for greater than
# M for megabytes, G for Gigabytes, k for kilobytes, etc. 
{% endhighlight %}

##### How to know your commands better. 
Navigation in a local environment with a lot of ```.bashrc``` options might be easy. However, it is not that accessible in most cases where you need to work on a remote Linux environment. How to navigate on the black-green screen largely categorizes your productivity level. Here are some commands that are either well-known or well-used. 
{% highlight shell %}
########################
# Navigation
ctrl + a  # go to the start of the command
ctrl + e  # go to the end of the command
ctrl + k  # delete from cursor to the end of the command line
ctrl + u  # delete from cursor to the start of the command line
ctrl + w  # delete from cursor to start of word
alt + b   # move backward one word (needs to configure alt as esc+)
alt + f   # move forward one word
ctrl + f  # move forward one character
ctrl + b  # move backward one character
ctrl + d  # delete character under the cursor
ctrl + h  # delete character before the cursor
########################
# Command History
ctrl + r  # search the history backwards
ctrl + g  # escape from history searching mode
ctrl + p  # previous command in history
ctrl + n  # next command in history
########################
# Control
ctrl + l  # clear the screen
ctrl + s  # stops the output to the screen
{% endhighlight %}
