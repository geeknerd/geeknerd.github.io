---
layout: post
title: Alfred 3 Would Like To Access Your Contacts
date: 2018-06-18
modifited: 2018-06-18
comments: true
pinned: true
tags: [MacOS]
---
After "upgrading" the PowerPack of Alfred 3, it asks for contacts permission everytime after reboot. Open terminal and re-do the signature:
~~~ shell
sudo codesign -f -d -s - /Applications/Alfred\ 3.app/Contents/Frameworks/Alfred\ Framework.framework/Versions/A/Alfred\ Framework  
~~~
On success it should return:
~~~ shell
/Applications/Alfred 3.app/Contents/Frameworks/Alfred Framework.framework/Versions/A/Alfred Framework: replacing existing signature  
~~~
Peace ...

BTW.  
Happy *Dragon Boat Festival*