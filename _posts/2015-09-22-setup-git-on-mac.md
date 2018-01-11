---
layout: post
title: Set Up Git on Mac OS X
date: 2015-09-22
comments: true
pinned: true
tags: [MacOS,git]
---

```1.``` First, you need to download the latest version of Git from [here](http://git-scm.com/downloads).

```2.``` Then you need to configure your global name and email address through the following commands, using Terminal or similar apps of your choice.
{% highlight bash %} 
$ git config --global user.name "YOUR NAME"
$ git config --global user.email "YOUR EMAIL ADDRESS"
{% endhighlight %}

```3.``` Recommended workaround if cloning with HTTPS, so you could cache your GitHub password using a credential helper.

Check if the ```osxkeychina credential helper``` is installed by running:
{: .textbox}
    
{% highlight bash %} 
$ git credential-osxkeychain
# Test for the cred helper
# Usage: git credential-osxkeychain <get|store|erase>
{% endhighlight %}

If it isn't installed, download and install it. 
{: .textbox}

{% highlight bash %} 
$ git credential-osxkeychain
# Test for the cred helper
# git: 'credential-osxkeychain' is not a git command. See 'git --help'.
$ curl -s -O \
https://github-media-downloads.s3.amazonaws.com/osx/git-credential-osxkeychain
# Download the helper
$ chmod u+x git-credential-osxkeychain
# Fix the permissions on the file so it can be run
{% endhighlight %}

And you need to move it to the same directory with Git.
{: .textbox}

{% highlight bash %} 
$ sudo mv git-credential-osxkeychain \
"$(dirname $(which git))/git-credential-osxkeychain"
# Move the helper to the path where git is installed
# Password: [enter your password]
{% endhighlight %}

Configure the ```osxkeychain```
{: .textbox}

{% highlight bash%} 
$ git config --global credential.helper osxkeychain
# Set git to use the osxkeychain credential helper
{% endhighlight %}

```4.``` At any point you want to remove the credential or modify it, open ```Keychain Access``` on your Mac, search for ```github.com```, the *Internet Password* is the entry you're looking for. Or you could use the command to erase it:

{% highlight bash %} 
$ git credential-osxkeychain erase
host=github.com
protocol=https
# [Press Return]
{% endhighlight %}
