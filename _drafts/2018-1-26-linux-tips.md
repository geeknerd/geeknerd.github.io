---
layout: post
title: Linux Command Tips
excerpt: "A slowly built up of some useful but might be rarely used Linux tips."
date: 2018-01-26
modifited: 2018-01-26
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