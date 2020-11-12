
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

-- GROUP BY CHALLENGE 1
-- we have two staff members, with staff IDS 1 and 2. 
-- we want to give a bonus to the staff member that handled the most payments(most in terms of number payments processed, not total dollar amount).
-- how many payments did each staff member handle and who gets the bonus?
select * from payment
select staff_id, count(*) from payment group by staff_id 

-- GROUP BY CHALLENGE 2
-- corporate HQ is conducting a study on the relationsship between replacement cost and a movie MPAA rating(ex: G, PG, R, etc...)
-- what is the average replacement cost per MPAA rating?
-- note: you may need to expand the AVG column to view the results

select rating, round(avg(replacement_cost),2) from film group by rating 

---- GROUP BY CHALLENGE 3
-- we are running a promotion to reward our top 5 customers with coupons.
-- what are the customer ids ofthe top 5 customers by total spend?
select customer_id, sum(amount) from payment group by customer_id order by sum(amount) desc limit 5

-- HAVING CHALLENGE 1
-- We are launching a platinum service for our most loyal customers. we will assign platinum status to customers that have had 40 or more transacction payments.
-- what customer_ids are eligible for platinum status?
select * from payment
select customer_id, count(customer_id) from payment group by customer_id having count(customer_id) >= 40

--HAVING CHALLENGE 2
-- What are the customer ids of customers who have spent more than $100 in payment transactions with our staff_id member 2?
select customer_id, sum(amount) from payment where staff_id = 2 group by customer_id having sum(amount) > 100

-- ASSESSMENT TEST QUESTION 1
-- Return the customer IDS of customers who have spent at least $110 with the staff member who has an ID of 2
-- the answer should be customers 187 and 148
select customer_id, sum(amount) from payment where staff_id = 2 group by customer_id having sum(amount) >= 110


-- ASSESSMENT TEST QUESTION 2
-- How many films begin with the letter J?
-- the answer should be 20
select count(title) from film where title like 'J%'

-- ASSESSMENT TEST QUESTION 3
-- What customer has the highest customer ID number whose name starts with an 'E' and has an address ID lower than 500?
-- The answer is Eddie Tomlin
select first_name, last_name from customer where first_name ilike 'e%' and address_id < 500 order by customer_id desc limit 1