
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

-- JOIN CHALLENGE TASK 1
-- california sales tax laws have changed and we need to alert our customers to this through email
-- what are the emailof the customers who live in california?
select district, email from address join customer on address.address_id = customer.address_id where address.district = 'California'

-- Join Challenge 2
-- a customer walks in and is a huge fan of the actor 'Nick Wahlberg' and wants to know which movies he is in.
-- get a list of all the movies nick wahlberg has been in
select title, first_name, last_name from film_actor join actor on film_actor.actor_id = actor.actor_id join film on film_actor.film_id = film.film_id where first_name = 'Nick' and last_name = 'Wahlberg'

SECTION 6: ADVANCE SQL COMMANDS
show all
show timezone
select now()
select timeofday() --same as select now() but as a string
select  current_date

-- timestamp and extract challenge 1
-- during which months did payments occur?
-- format your answer to return back the full month name
select distinct(to_char(payment_date, 'MONTH'))
from payment

--timestamp and extract challenge 2
-- how many payments occured on a monday?
select count(to_char(payment_date, 'dy'))
from payment
where to_char(payment_date, 'dy') = 'mon'

select * 
from film

select round(rental_rate/replacement_cost,4)*100 as percent_cost
from film

select 0.1 * replacement_cost as depost 
from film

select * from customer

select length(first_name)
from customer

select first_name || ' ' || last_name as full_name
from customer

select lower(left(first_name,1) || last_name || '@gmail.com') as custom_email
from customer

select * from film

select title, rental_rate 
from film
where rental_rate > (select avg(rental_rate) from film)

select * from rental

select film_id, title
from film
where film_id in
(select inventory.film_id 
from rental
inner join inventory on inventory.inventory_id = rental.inventory_id
where return_date between '2005-05-29' and '2005-05-30')
order by title

select first_name, last_name
from customer as c
where exists 
(select * from payment as p
 where p.customer_id = c.customer_id
 and amount > 11)

 select f1.title, f2.title, f1.length
from film as f1
join film as f2 on 
f1.film_id != f2.film_id
and f1.length = f2.length

--sql assessment test 2 question 1
--how can you retrieve all of the information from the cd.facilities table?
select * from cd.facilities

--sql assessment test 2 question 2
-- you want to print out a list of all of the facilities and their cost to members. how would you retreive a list of only facility names and cost?
select name, membercost from cd.facilities

--sql assessment test 2 question 3
-- how can you produce a list of facilities that charge a fee to members?
select * from cd.facilities where membercost > 0

--sql assessment test 2 question 4
-- how can you produce a list of facilities that charge a fee to members and that fee is less than 1/50th of the monthly maintence cost?
-- return the facid, facility name, member cost and monthly mantenance of the facilities in question
select facid, name, membercost, monthlymaintenance from cd.facilities where membercost > 0 and membercost < (monthlymaintenance * 0.02)

--sql assessment 2 question 5
-- how can you produce a list of all facilities with the word 'Tennis' in their name?
select * from cd.facilities where name like '%Tennis%'

--sql assessment 2 question 6
--how can you retreive the data of facilities with ID 1 and 5
select * from cd.facilities where facid in(1,5)

--sql assessment 2 question 7
--how can you produce a list of members who joined after the start of september 2012? return the memid, surname, firstname and joindate of the members in question
select memid, surname, firstname, joindate  from cd.members where joindate > '2012-09-01'

--sql assessment 2 question 8
-- how can you produce an ordered list on the first 10 surnames in the members table? the list must not contain duplicates
select distinct(surname) from cd.members order by surname limit 10

--sql assessment 2 question 9
-- you'd like to get the signup date of your last member. how can you retrieve this info?
select * from cd.members
select joindate from cd.members order by joindate desc limit 1
--sql assessment 2 question 10
-- produce a count of the number of facilities that have a cost ot guests of 10 or more
select count (guestcost) from cd.facilities where guestcost > 10

--sql assessment 2 question 11
--produce a list of the total number of slots booked perfacility in the month of September 2012. Produce an output table consisting of the facilityid and slots, sorted by the number of slots.
SELECT facid, SUM(slots) AS Total_Number_of_Slots
FROM cd.bookings
WHERE cd.bookings.starttime BETWEEN '2012-09-01' AND '2012-09-30'
GROUP by facid
ORDER BY SUM(slots);

--sql assessment 2 question 12
--produce a list of facilities with more than 1000 slots booked. Produce an output table consisting of facility id and total slots sorted by facility id
--each one has a facid, so we probably have to count the total slots associated to each facid
select facid, sum(slots) from cd.bookings group by facid having sum(slots) > 1000 order by facid

--sql assessment 2 question 13
-- how can you produce a list of the start times for bookings for tennis courts, for the date'2012-09'21'? return a list of start time and facility name parings, ordered by the time

--my notes
--join by facid, probably inner join since we want them to have matching facid to the facilities with tennis court in them
--and then we have to use the starttime column from bookings for the date

select starttime, "name" from cd.bookings join cd.facilities on cd.bookings.facid = cd.facilities.facid where cd.facilities.name like 'Tennis Court%' and starttime BETWEEN '2012-09-21 00:00:00' AND '2012-09-21 23:59:59' order by starttime

--sql assessment 2 question 14
--how can you produce a list of the start times for bookings by members named 'David Farrell'
select starttime from cd.bookings join cd.facilities on cd.bookings.facid = cd.facilities.facid join cd.members on cd.bookings.memid = cd.members.memid where firstname = 'David' and surname = 'Farrell'


 SQL DATA TYPES
 -booleans
 -characters
 -numeric
 -temporal : date, time, time stamp and interval

 create table account_job (
	user_id integer references account(user_id),
	job_id integer references job(job_id),
	hire_date timestamp
)

select * from account
insert into account (username, password, email, created_on)
values
('Jose', 'password','jose@mail.com', current_timestamp)

select * from job
insert into job (job_name)
values
('Scientist')

select * from account_job
insert into account_job(user_id, job_id, hire_date)
values
(1,1, current_timestamp)

//updating using values from another table (update join)
update account_job 
set hire_date = account.created_on
from account
where account_job.user_id = account.user_id

update account
set last_login = current_timestamp
returning email, created_on, last_login

delete from job
 where job_name = 'cowboy'
 returning job_id, job_name

 alter table information
rename to new_info

alter table new_info
rename column person to people

select* from new_info

alter table new_info
alter column people drop not null

alter table new_info
drop column people

insert into employees(
first_name,
	last_name,
	birthdate,
	hire_date,
	salary
)
values
('Sammy',
 'Smith',
 '1990-11-03',
 '2010-01-01',
 100
)

select * from employees

-- assessment test 3 question 1
create table students(
	teacher_id serial primary key,
	first_name varchar(50),
	last_name varchar(50),
	homeroom_number integer,
	department varchar(50),
	email varchar(500) unique,
	phone integer unique not null
)

alter table students add phone varchar(500) unique not null

select * from students

insert into students (
	first_name,
	last_name,
	student_id,
	phone,
	graduation_year,
	homeroom_number
)
values
('Mark',
 'Watney',
 1,
 '777-555-1234',
 2035,
 5
)