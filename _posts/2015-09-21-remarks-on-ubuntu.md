---
layout: post
title: Some Remarks on Ubuntu 14.04.03
date: 2015-09-21
tags: [Linux]
comments: true
pinned: true
---


Click on icon to minimize an app/window does not come with Ubuntu 14.04.03, to enable the feature either one can use [compizconfig settings manager][1] to set it from Unity Plugin or use the following command:
{% highlight bash %}
gsettings set org.compiz.unityshell:/org/compiz/profiles/unity/plugins/unityshell/ launcher-minimize-window true
{% endhighlight %}

To revert the change:
{% highlight bash %}
gsettings set org.compiz.unityshell:/org/compiz/profiles/unity/plugins/unityshell/ launcher-minimize-window false
{% endhighlight %}

[1]: https://apps.ubuntu.com/cat/applications/compizconfig-settings-manager/
