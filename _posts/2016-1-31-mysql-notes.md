---
layout: post
title: MySQL Syntax Notes
date: 2016-01-31
comments: true
pinned: true
tags: [MySQL]
---

* When creating a database, the default behavior of case sensitivity is set by the collation used. Changing a collation using a query could only use the same ```CHARACTER SET```. 
To use a case sensitive wildcard in a ```SELECT``` query, it is simpler to use ```BINARY``` operator after the ```LIKE```. Like the one below,
{% highlight MySQL %}
SELECT prod_name, prod_price, prod_id FROM products WHERE prod_name LIKE BINARY'%Anvil%';
{% endhighlight %}
The result is:

![MySQL CS]({{site.url}}/img/mysql-cs.png)

* It is important to note that, in addition to matching one or more characters, ```%``` also matches zero characters. ```%``` represents zero, one, or more characters at the specified location in the search pattern.

* ```BINARY``` works the same in a regular expression match. Like:
{% highlight MySQL %}
WHERE prod_name REGEXP BINARY 'JetPack .000';
{% endhighlight %}

* ```^``` will negate everything in the ```[]```. Therefore, ```[^123]``` will match characters other than 1 and 2 and 3. Same as ```[^1-3]```.

Omitting ```FROM``` clause after ```SELECT``` simply tests the function and calculation. 

* **SOUNDEX** matches patterns that sound similar to the specified value, like the following:

{% highlight MySQL %}
SELECT cust_name, cust_contact
FROM customers
WHERE Soundex(cust_contact) = Soundex('Y Lie');
{% endhighlight %}	

![MySQL SoundEX]({{site.url}}/img/mysql-sex.png)

* To use a full-text search, specify ```FULLTEXT(<column_name>)``` in ```CREATE TABLE``` query and set ```ENGINE=MyISAM```. 

Use ```BINARY``` mode for case sensitive search. 

Syntax is as: 
{% highlight MySQL %}
SELECT note_text FROM productnotes WHERE Match(note_text) Against('rabbit');
{% endhighlight %}

* Use ```WITH QUERY EXPANSION``` to full-text search for related rows based on first search for the keyword. 
``` MySQL
SELECT note_text 
FROM productnotes 
WHERE Match(note_text) Against('anvils' WITH QUERY EXPANSION);
```