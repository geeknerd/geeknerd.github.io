---
layout: post
title: MySQL Syntax Notes
date: 2016-01-13
comments: true
pinned: true
tags: [MySQL]
---

When creating a database, the default behavior of case sensitivity is set by the collation used. Changing a collation using a query could only use the same ```CHARACTER SET```. 
To use a case sensitive wildcard in a ```SELECT``` query, it is simpler to use ```BINARY``` operator after the ```LIKE```. Like the one below,
{% highlight MySQL %}
SELECT prod_name, prod_price, prod_id FROM products WHERE prod_name LIKE BINARY'%Anvil%';
{% endhighlight %}
The result is:

![MySQL CS]({{site.url}}/img/mysql-cs.png)

It is important to note that, in addition to matching one or more characters, ```%``` also matches zero characters. ```%``` represents zero, one, or more characters at the specified location in the search pattern.

```BINARY``` works the same in a regular expression match. Like:
{% highlight MySQL %}
WHERE prod_name REGEXP BINARY 'JetPack .000';
{% endhighlight %}

```^``` will negate everything in the ```[]```. Therefore, ```[^123]``` will match characters other than 1 and 2 and 3. 