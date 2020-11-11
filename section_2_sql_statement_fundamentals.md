TEST TEST TEST

--Challenge: SELECT
select first_name, last_name, email from customer limit 100

--Challenge: select distinct
select distinct rating from film

--Challenge: select where 1
select email from customer where first_name = 'Nancy' and last_name = 'Thomas'
--Challenge: select where 2
select description from film where title = 'Outlaw Hanky'

--Challenge: select where 3
select phone from address where address = '259 Ipoh Drive'


CHALLENGE ORDER BY
-- challenge 1
select * from payment
select customer_id from payment order by payment_date asc limit 10;

-- challenge 2
select * from film
select title, "length" from film order by "length" limit 5;

-- bonus challenge
select count (title) from film where "length" <= 50;

--General Challenge 1 - challenge 1
-- how many payment transactions were greater than $5.00
select * from payment
select count (amount) from payment  where amount > 5.00 

--General Challenge 1 - challenge 2
select * from actor
select count (first_name) from actor where first_name like 'P%'

--General Challenge 1 - challenge 3
-- How many unique districst are our customers from
select * from address
select count(distinct(district)) from address

--General Challenge 1 - challenge 4
--Retreive the list of names for those distinct districts from the previous quesiton
select distinct(district) from address 

--General Challenge 1 -- challenge 5
--How many films have a rating of R and a replacement cost between $5 and $15
select * from film
select count(*) from film where rating = 'R' and replacement_cost between 5 and 15;

--General Challenge 1 -- challenge 5
-- How many films have the word Truman somewhere in the title?
select count(*) from film where title like '%Truman%'