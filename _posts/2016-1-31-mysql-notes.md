---
layout: post
title: MySQL Syntax Notes
date: 2016-01-31
modified: 2016-02-02
comments: true
pinned: true
tags: [MySQL]
---

* When creating a database, the default behavior of case sensitivity is set by the collation used. Changing a collation using a query could only use the same ```CHARACTER SET```. 
To use a case sensitive wildcard in a ```SELECT``` query, it is simpler to use ```BINARY``` operator after the ```LIKE```. Like the one below,

{% highlight sql %}
SELECT prod_name, prod_price, prod_id FROM products 
WHERE prod_name LIKE BINARY'%Anvil%'
ORDER BY prod_name;
{% endhighlight %}

The result is:

![MySQL CS]({{site.url}}/img/mysql-cs.png)

* It is important to note that, in addition to matching one or more characters, ```%``` also matches zero characters. ```%``` represents zero, one, or more characters at the specified location in the search pattern.

* ```BINARY``` works the same in a regular expression match. Like:

~~~ sql
WHERE prod_name REGEXP BINARY 'JetPack .000';
~~~


* ```^``` will negate everything in the ```[]```. Therefore, ```[^123]``` will match characters other than 1 and 2 and 3. Same as ```[^1-3]```.

Omitting ```FROM``` clause after ```SELECT``` simply tests the function and calculation. 

* **SOUNDEX** matches patterns that sound similar to the specified value, like the following:

{% highlight sql %}
SELECT cust_name, cust_contact
FROM customers
WHERE Soundex(cust_contact) = Soundex('Y Lie');
{% endhighlight %}


![MySQL SoundEX]({{site.url}}/img/mysql-sex.png)

* To use a full-text search, specify ```FULLTEXT(<column_name>)``` in ```CREATE TABLE``` query and set ```ENGINE=MyISAM```. 

Use ```BINARY``` mode for case sensitive search. 

Syntax is as: 

~~~ sql
SELECT note_text FROM productnotes WHERE Match(note_text) Against('rabbit');
~~~

* Use ```WITH QUERY EXPANSION``` to full-text search for related rows based on first search for the keyword. 

~~~ sql
SELECT note_text 
FROM productnotes 
WHERE Match(note_text) Against('anvils' WITH QUERY EXPANSION);
~~~

* ```IN BOOLEAN MODE``` can include word, exclude word, modify word's ranking and search phrase in full-text search. 

~~~ sql
SELECT note_text
FROM productnotes
WHERE MATCH(note_text) AGAINST('+safe -rope* +(<combination)' IN BOOLEAN MODE);
~~~

This search matches words safe and combination, lowering the ranking of the latter, and excludes any words that start with "rope". 

* Use ```LOW_PRIORITY``` in ```INSERT```, ```UPDATE``` and ```DELETE``` statements to lower the priority of the statements so they don't affect performance. 

* Use ```IGNORE``` to continue updating table even error occurs. Such as:

~~~ sql
UPDATE IGNORE customers
SET cust_name = 'The Fudds',
    cust_email = 'elmer@fudd.com'
WHERE cust_id = 10005;
~~~

* Every row in a table must have a unique primary key value. If a single column is used for the primary key, it must be unique; if multiple columns are used, the combination of them must be unique.

* Use views to reuse SQL statements and simplify complex SQL operations. 
* Views contain no data themselves, the data are retrieved from other tables. Updating views essentially is updating the original table. 
* Performace will degrade if views contain complex statemtns like multiple joins and filters. 
Example of view:

~~~ sql
CREATE VIEW productcustomers AS
SELECT cust_name, cust_contact, prod_id 
FROM customers AS c JOIN orders AS o
ON c.cust_id = o.cust_id
JOIN orderitems AS oi ON o.order_num = oi.order_num;
~~~

* Procedure can be used to store one of more MySQL statements for future use. More or less like the functions in Java.
* Procudures execute faster than individual SQL statements, simplify complex operations and ensure data integrity. 
* Simplicity, Security, and Performance. 
* To use a command line utility, temporary delimiter should be used to overwrite ```;``` as follows:

~~~ sql
DELIMITER //
CREATE PROCEDURE productpricing(
OUT p1 DECIMAL (8,2),
OUT p2 DECIMAL (8,2),
OUT p3 DECIMAL (8.2)
)
BEGIN
SELECT MIN(prod_price) INTO p1 FROM products;
SELECT MAX(prod_price) INTO p2 FROM products;
SELECT AVG(prod_price) INTO p3 FROM products;
END; //
DELIMITER ;
~~~

* All MySQL variable names must begin with ```@```.

* A ```cursor``` is a query stored on the MySQL server as the result set retrieved by a ```SELECT``` statement. Cursor is used to scroll or browse through the data as needed, something that can't be achieved through single ```SELECT``` statement. 
* MySQL cursors may only be used within stored procedures(and functions).
* Cursor needs to be opened after declaration and closed after done. 
* Local variables defined with ```DECLARE``` must be defined before any cursors or handlers are defined, and handlers must be defined after any cursors.

~~~ sql
CREATE PROCEDURE processorders()
BEGIN

	-- Declare local variables
    DECLARE done BOOLEAN DEFAULT 0;
    DECLARE o INT;
    DECLARE t DECIMAL (8,2);
    
    -- Declare the cursor
    DECLARE ordernumbers CURSOR
    FOR
    SELECT order_num FROM orders;
	
    -- Declare continue handler
    DECLARE CONTINUE HANDLER FOR SQLSTATE '02000' SET done = 1;
    
    -- Create a table to store the results
    CREATE TABLE IF NOT EXISTS ordertotals
		(order_num INT, total DECIMAL (8,2));
        
	-- Open the cursor
    OPEN ordernumbers;
    
    -- Loop through all rows
    REPEAT
		
        -- Get order number
        FETCH ordernumbers INTO o;
        
        -- Get the total for this order
        CALL ordertotal(o, 1, t);
        
        -- Insert order and total into ordertotals
        INSERT INTO ordertotals(order_num, total)
        VALUES(o, t);
        
	-- End of loop
    UNTIL done END REPEAT;
    
    -- Close the cursor
    CLOSE ordernumbers;
    
END;
~~~

* A *trigger* is a MySQL statement (or a group of statements enclosed within BEGIN and END statements) that are automatically executed by MySQL in response to ```DELETE```, ```INSERT``` or ```UPDATE```.
* A virtual table named ```NEW``` is used to access the rows when using ```INSERT``` trigger, like:

~~~ sql
CREATE TRIGGER neworder AFTER INSERT ON orders
FOR EACH ROW SELECT NEW.order_num;
~~~

* **In MySQL, triger can not return a resultset, so the above will not work. Either use a procedure or use a ```SET``` in a triger could solve the problem.**
* Use transactions for blocks that must be executed as a batch without failure. 

~~~ sql 
START TRANSACTION;
DELETE FROM orderitems WHERE order_num = 20010;
SAVEPOINT delete1;
DELETE FROM orders WHERE order_num = 20010;
COMMIT;
~~~

* Use ```AUTOCOMMIT``` to change the commit behavior of statement, which is defaulted as implicitly commit. The ```AUTOCOMMIT``` flag is per connection, not server-wide. 

~~~ sql
SET autocommit=0;
~~~

* Use ```IFNULL()``` function to return a different value when retrieve ```NULL``` values from the table. 

~~~ sql 
SELECT  
IFNULL(CONCAT(cust_name,' has email: ', cust_email), CONCAT(cust_name,' has no email'))
AS cust_info  FROM customers;
~~~

*Working script*

{% gist geeknerd/mysql_crash_course.sql %}