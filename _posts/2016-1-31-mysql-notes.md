---
layout: post
title: MySQL Syntax Notes
date: 2016-01-13
comments: true
pinned: true
tags: [MySQL]
---

When creating a database, the default behavior of case sensitivity is set by the collation used. Changing a collation using a query could only use the same ```CHARACTER SET```. 
To use a case sensitive wildcard in a ```SELECT``` query, it is simpler to use BINARY operator after the ```WHERE```. Like the one below,
{% highlight MySQL %}
SELECT prod_name, prod_price, prod_id FROM products WHERE BINARY prod_name LIKE '%anvil%';
{% endhighlight %}
The result is:
+--------------+------------+---------+
| prod_name    | prod_price | prod_id |
+--------------+------------+---------+
| .5 ton anvil |       5.99 | ANV01   |
| 1 ton anvil  |       9.99 | ANV02   |
| 2 ton anvil  |      14.99 | ANV03   |
+--------------+------------+---------+