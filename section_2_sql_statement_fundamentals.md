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