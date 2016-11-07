# w7d1-make-SQL

How many users are there?
Answer: sqlite> select count(*) from users;
count(*)  
----------
50 

What are the 5 most expensive items?
Answer: sqlite> select price from items order by price desc;
price     
----------
9984      
9859      
9790      
9390      
9341


What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
Answer:select category, price from items where category like 'book'; (didn't change when using '%book%')
Books       1496 


Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
Answer: first_name  last_name   id        
----------  ----------  ----------
Corrine     Little      40        

select user_id, street, city, state, zip from addresses where street like '6439 Zetta Hills';
user_id     street            city        state       zip       
----------  ----------------  ----------  ----------  ----------
40          6439 Zetta Hills    Willmouth   WY          15029     
40          54369 Wolff Forges  Lake Bryon  CA          31587   

so yes, Corrine Little has two addresses.



Correct Virginie Mitchell's address to "New York, NY, 10108".
Answer: update addresses set city='New York', state='NY', zip='10108' where user_id=39;
sqlite> select * from addresses;

41          39          12263 Jake Crossin  New York    NY          10108     
42          39          83221 Mafalda Cany  New York    NY          10108 


How much would it cost to buy one of each tool?
Answer: select category, price from items where category like '%Tools%';
category               price     
---------------------  ----------
Beauty, Shoes & Tools  7476      
Industrial & Tools     2851      
Tools                  1107      
Garden, Toys & Tools   798       
Tools, Garden & Movie  3335      
Tools, Clothing & Toy  615       
Tools, Jewelery & Ind  7606      
Tools, Garden & Games  1913      
Tools & Computers      2768      
Sports & Tools         3160      
Tools                  5437      
Games, Sports & Tools  5210      
Tools                  839       
Books, Toys & Tools    2377      
Tools & Kids           985       
sqlite> select category, sum(price) from items where category like '%Tools%';
category      sum(price)
------------  ----------
Tools & Kids  46477  


How many total items did we sell?
Answer: select sum(quantity) from orders ;
sum(quantity)
-------------
2125          


How much was spent on books?
Answer: select category, sum(price) from items where category like '%Books%';
category      sum(price)
------------  ----------
Toys & Books  59241


Simulate buying an item by inserting a User for yourself and an Order for that User.
Answer: insert into orders values ('378','51','100','4', datetime());
sqlite> select * from orders;
id          user_id     item_id     quantity    created_at                
----------  ----------  ----------  ----------  --------------------------
378         51          100         4           2016-11-07 18:54:37

insert into users values ('100','Jeff','Bumgardner', 'jeff@gmail.com');
sqlite> select * from users;
id          first_name  last_name   email                     
----------  ----------  ----------  --------------------------
100         Jeff        Bumgardner  jeff@gmail.com 
