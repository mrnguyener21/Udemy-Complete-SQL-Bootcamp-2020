<!-- challege: select where
select * from film
select description from film where title = 'Outlaw Hanky'

select phone from "address" where address = '259 Ipoh Drive' 
 -->

<!-- 
Challenge: ORDER BY
select phone from "address" where address = '259 Ipoh Drive'  

select phone from "address" where address = '259 Ipoh Drive' 

select count(length) from film where length <= 50
-->

<!-- General Challenge 1
select count(amount) from payment where amount > 5

select count(*) from actor where first_name like 'P%'

select count(distinct(district)) from address

select distinct(district) from address

select count(*) from film where rating = 'R' and replacement_cost between 5 and 15

select count(*) from film where title like '%Truman%' -->

<!-- Challenge Group BY

--we have 2 staff members, with staff IDs 1 and 2. We want to give a bonus to the stff member that handled the most payments.(most in terms of number ofpayments processed, not total dollar amount).--
-- how many payments did each staff member handle and who gets the bonus--
select count(payment_id) from payment group by staff_id

--Corporate HQ is conducting a study on the relationship between replacement cost and a movie MPAA rating(G, PG, R ,ETC)--
--What is the average replacement cost perr MPAA rating 
--NOTE: You may need to expand the AVG column to view correct results
select rating, avg(replacement_cost) from film group by rating

--We are running a promotion to reward our top 5 customers with coupons.--
--what are the customer ids of the top 5 customers by total spend?
select customer_id, sum(amount) from payment group by customer_id order by sum(amount) desc limit 5 -->

<!-- --ASSESSMENT TEST 1 --
-- 1) Return the customer IDs of customers who have spent at least $110 with the staff member who has an ID of 2. --
-- The answer should be customers 187 and 148 --
select customer_id, sum(amount) from payment where staff_id = 2 group by customer_id having sum(amount) >=110

-- 2) How many films begin with the letter J?--
-- The answer should be 20 --
select count(title) from film where title like 'J%'

--3) What customer has the highest customer ID number whose name starts with an 'E' and has an address ID lower than 500?
-- The answer is Eddie Tomlin
select first_name, last_name from customer where address_id < 500 and first_name like 'E%' order by customer_id DESC limit 1 -->

<!-- JOIN Challenge Task

-- california sales tax laws have changed and we need to alert our customers to this through email.
-- What are the emails of the customers who live in California?
select * from address
select * from customer

select district, email from address join customer on address.address_id = customer.address_id where district = 'California'

--A customer walks in and is ah uge fan of the actor 'Nick wahlberg' and wants to know which movies he is in.--
-- get a list of all the movies 'Nick Wahlberg' has been in. --
-- We want title, first name and last name --
select * from actor
select * from film
select * from film_actor

select film.title, actor.first_name, actor.last_name from film join film_actor on film.film_id = film_actor.film_id join actor on film_actor.actor_id = actor.actor_id where actor.first_name = 'Nick' and  actor.last_name = 'Wahlberg' -->

<!-- TIMESTAMPS AND EXTRACT
During which months did payments occur?--
--Format your answer to return back the full month name--
select distinct(to_char(payment_date,'month')) from payment

--How many payments occured on a monday?--
select count(*) from payment where extract(dow from payment_date) = 1 -->

ASSESSMENT 2
-- How can you retrieve all the info from the cd.facilities table?

--You want to print out a list of all of the facilities and their cost to members.
--How would you retrieve a list of only names and cost?


--How can you produce a list of facilities that charge a fee to members?

--How can you produce a list of facilities that charge a fee to members, and that fee is less  than 1/50th of the  monthly maintenance cost?
-- Return the facid, facility name, member cost and monthly maintenence of the facilities in question.


--How can you produce a list of all facilities with the word 'Tennis' in their name?

--How can you retrieve the details of facilities with ID 1 and 5?
--Try to do it without using the OR operator.

--How can you produce a list of members who joined after the start of september 2012?
--Return the memid, surname, firstname, and joindate of the members in question?


--How can you produce an ordered list of  the first 10 surnames in the memebrs table?
--The table must not contain duplicates.

--You'd like to get the sign up date of your last member. How can you retrieve this information?

--Produce a count of the number of facilities thatt have a cost ot guests of 10 or more.

--Produce a list of the total number of slots booked pper facility in the month of september 2012.
--Produce an output table consisting of facility id and slots, sorted by the number of slots.

--Produce a list of facilities with more than 1000 slots booked. 
--Produce an output table consisting of facility id and total slots, sorted by facility id.


--How can you produce a list of the start times for bookings for tennis courts, for the date '2012-09-21'?
--Return a list of start time aand facility name pairings, ordered by the time?

--How can you produce a list of the start times for bookings by members named 'David Farrell'?