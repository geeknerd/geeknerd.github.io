---
layout: post
title: Remarks on ns-3 3.23
date: 2015-09-14
modified: 2015-09-15
tags: [Linux, ns-3]
category: updates
pinned: true
---

If the ns-3 is built through a tarball, an environment variable can save some time to run a script from everywhere instead of specifying the directory of `waf`.


{% highlight bash %}
$ export NS3DIR="$PWD"
$ function waff { cd $NS3DIR && ./waf $* ; }

$ cd scratch
$ waff build
{% endhighlight %}

If you have the full ns-3 repository this little gem is a start:
{% highlight bash %}
$ cd $(hg root) && ./waf ...
{% endhighlight %}

Even better is to define this as a shell function:
{% highlight bash %}
$ function waff { cd $(hg root) && ./waf $* ; }

$ waff build
{% endhighlight %}
