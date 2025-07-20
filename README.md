# In-between-IN-create-new-column---SQL
In between, IN, create new column - SQL


Select * from orders;

-- To get distinct value of a column
select distinct [ship mode] from orders;

Select distinct [order date] from orders
order by [order date];

-- i want to select two column
select distinct [order date] , [ship mode] from orders;

-- select whole data and order it by order date
select * from orders order by [order date];

-- if the two rows contain same data, means duplicate, we can distinct it as weel, but in this data this will not happen, because 
-- every row is unique, as row id is different
select distinct * from orders;

                                                              -- FILTERS --
select * from orders 
where [ship mode] = 'first class';

select * from orders 
where [order date] = '2015-07-30 00:00:00.000';

select * from orders 
where [order date] > '2015-07-30 00:00:00.000';

select * from orders 
where quantity = 4;

select * from orders 
where quantity > 5;

select * from orders 
where quantity !> 5; -- this is not equal to 

select [customer name], quantity from orders 
where quantity >= 5 order by quantity desc;

select top 3 [order date], quantity 
from orders 
where quantity >= 5 
order by quantity desc;

-- Date and string we will put inside inside single colon (' ') but integer and number we will not put inside colon.

select * from orders
where [order date] between '2014-06-09' and '2015-01-31' 
order by [order date] desc;

select [ship mode], [customer name] from orders
where Quantity between '5' and '6' 
order by [order date] desc;

-- how to use in operator
select [customer name], quantity from orders 
where quantity in (3,5);

-- not necessary to give two or more values, we can give only one value in (in operator) , value must mention inside brackets () 
select * from orders 
where [order date] in ('2015-10-11');

-- how to use not in operator
select * from orders 
where [ship mode] not in ('standard class');

select distinct [ship mode] from orders 
where [ship mode] not in ('standard class');

select [ship mode], [customer name],state from orders 
where [ship mode] in ('first class','second class') and state = 'florida';

-- greater then (>) also work with string
select distinct [ship mode]  from orders 
where [ship mode] > ('first class');

-- we can also use (or) operator, either one of the condition is satisfy, we will get output
select [row ID] , [ship mode] from orders
where [row ID] = 1 or [ship mode] = 'second class'; 

                                      -- creating a new column in SQL -- 
select sales+profit as total, * from orders
where [row id] < 5; 

-- now i want to see this new column at the end
select *,sales+profit as total from orders
where [row id] < 5; 


-- Pattern Matching Like opeartor
-- All the customer whose name start with B
select [row id], [order date] , [customer name] from orders
where [customer name] like 'B%'

-- All the customer whose name start with C
select [row id], [order date] , [customer name] from orders
where [customer name] like '%C'

-- All the customer whose name start with C and end with B
select [row id], [order date] , [customer name] from orders
where [customer name] like 'C%B'

-- start with anything and end with anything but must contain (rai) anywhere in between
select [row id], [order date] , [customer name] from orders
where [customer name] like '%rai%'

-- must start with 'r' , then after one letter must contain 'a' then end with 'n'
select [row id], [order date] , [customer name] from orders
where [customer name] like 'R_a%n';

-- If case sensitive is enabled
select [row id], [order date] , [customer name], upper([customer name]) as capital_name from orders
where upper([customer name]) like '%rAI%'

-- what if any customer name is Craig % Carreira (it include special character in between)
select [row id], [order date] , [customer name] from orders
where [customer name] like 'C%A'escape '%'; -- it only work when special character is '%' 

-- First character should be C, second character either A or L
select [row id], [order date] , [customer name] from orders
where [customer name] like 'C[AL]%';


-- First character should be C, but second character should not be (A or L)
select [row id], [order date] , [customer name] from orders
where [customer name] like 'C[^AL]%';

-- range (second charcter could be anuthing in between A-D)
select [row id], [order date] , [customer name] from orders
where [customer name] like 'C[A-D]%';

-- Below query does not show data below (CA-2015)
select [order id], [order date] , [customer name] from orders
where [order id] like 'CA-201[5-8]%';
