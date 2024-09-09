use employee;
#Practice project 2: Air Cargo Analysis

#Write a query to create route_details table using suitable data types for the fields, such as route_id, flight_num, origin_airport, 
#destination_airport,aircraft_id, and distance_miles. Implement the check constraint for the flight number and unique constraint for the route_id fields. Also, make sure that the distance miles field is greater than 0.
create table route1 (route_id int not null unique, flight_num int not null check(flight_num>0), origin_airport varchar(12), 
destination_airport varchar(12) ,aircraft_id int , distance_miles int check (distance_miles >0), primary key(route_id));

#Write a query to display all the passengers (customers) who have travelled in routes 01 to 25. Take data  from the passengers_on_flights table.
select concat(first_name,' ',last_name)  ,route_id from passengers_on_flights p  join  customer c on c.customer_id =p.customer_id 
order by route_id limit 26;

#Write a query to identify the number of passengers and total revenue in business class from the ticket_details table.
select count(customer_id)as no_of_passengers, sum(no_of_tickets* Price_per_ticket)  as total_revenue from ticket_details where class_id ='Bussiness';

#Write a query to display the full name of the customer by extracting the first name and last name from the customer table.
select concat(first_name,' ',last_name) as full_name from customer;
#Write a query to extract the customers who have registered and booked a ticket. Use data from the customer and ticket_details tables.
select c.customer_id,no_of_tickets , concat(first_name,' ',last_name),p_date from customer as  c inner join ticket_details as t on c.customer_id =t.customer_id where no_of_tickets >0 ;

#Write a query to identify the customer’s first name and last name based on their customer ID and brand (Emirates) from the ticket_details table.
select  first_name,last_name from customer where customer_id in (select customer_id from ticket_details where brand ='emirates');

#Write a query to identify the customers who have travelled by Economy Plus class using Group By and Having clause on the passengers_on_flights table.
select * from passengers_on_flights group by customer_id having class_id='economy plus';

#Write a query to identify whether the revenue has crossed 10000 using the IF clause on the ticket_details table.
select if (sum(Price_per_ticket) >10000, 'revenue is greater than 10000','revenue is less than 10000') 
check_if_revenue_greater_than from ticket_details;

#Write a query to create and grant access to a new user to perform operations on a database.
create user `John_123` identified by '123456';
GRANT SELECT ON emp.* TO `John_123`;
GRANT INSERT ON emp.* TO `John_123`;
GRANT UPDATE ON demo.* TO `John_123`;
GRANT DELETE ON emp.* TO  `John_123`;
GRANT EXECUTE ON emp.* TO `John_123`;
show grants for `John_123`;

#Write a query to find the maximum ticket price for each class using window functions on the ticket_details table.
select * , max(Price_per_ticket) over (partition by class_id) max_ticket from ticket_details ;

#Write a query to extract the passengers whose route ID is 4 by improving the speed and performance of the passengers_on_flights table.
create index route_id on passengers_on_flights(route_id);
select * from passengers_on_flights where route_id='04';

#For the route ID 4, write a query to view the execution plan of the passengers_on_flights table.
select * from passengers_on_flights where route_id='04';

#Write a query to calculate the total price of all tickets booked by a customer across different aircraft IDs using rollup function.
SELECT  customer_id ,aircraft_id, sum( Price_per_ticket)  as total_price from ticket_details GROUP BY customer_id, aircraft_id WITH ROLLUP;
#Write a query to create a view with only business class customers along with the brand of airlines.
CREATE VIEW VIEW_CUST3 AS SELECT  customer_id , brand,class_id from ticket_details where class_id='bussiness';
SELECT * FROM VIEW_CUST3 ;
 
#Write a query to create a stored procedure to get the details of all passengers flying between a range of routes defined in run time. Also, return an error message if the table doesnt exist.
delimiter //
create  procedure stored_pass6 ( in range1 int, in range2 int) begin select * from passengers_on_flights where  route_id between  range1 and range2; end ; end// delimiter ;
call stored_pass5('1','25');

#Write a query to create a stored procedure that extracts all the details from the routes table where the travelled distance is more than 2000 miles.
delimiter //
create  procedure stored_dist4() begin select * from routes where distance_miles > 2000;  end// delimiter ;
call stored_dist4();

#Write a query to create a stored procedure that groups the distance travelled by each flight into three categories.
#The categories are, short distance travel (SDT) for >=0 AND <= 2000 miles, intermediate distance travel (IDT) for >2000 AND <=6500, 
#and long-distance travel (LDT) for >6500.
use employee;
drop procedure  if exists gettraveltype;
delimiter //
create procedure gettraveltype() begin declare dist int default 0; DECLARE  done bit default false; declare route_cur  cursor for
select distance_miles from routes; declare continue handler for not found set done =true; open route_cur;
create temporary table if not exists cep_routes_2(travel_type varchar(3)) as (select * from routes); 
while_label :while done = false do fetch route_cur into dist; 
if dist>=0 and dist <=2000 then update cep_routes_2 set travel_type ="SDT"
where distance_miles = dist;
elseif dist>2000 and dist <=6500 then update cep_routes_2 set travel_type ="IDT"
where distance_miles = dist;
 elseif dist>6500  then update cep_routes_2 set travel_type ="LDT" where distance_miles = dist;
 ELSE ITERATE WHILE_LABEL; end if ; end while while_label; 
 select * from cep_routes_2 order by distance_miles; end // 
 call gettraveltype();

#Write a query to extract ticket purchase date, customer ID, class ID and specify if the complimentary services are provided for the 
#specific class using a stored function in stored procedure on the ticket_details table.
#Condition:
#If the class is Business and Economy Plus, then complimentary services are given as Yes, else it is No

drop procedure if exists stored_purchase;
delimiter $$ 
create function  compli_services(  class_id  varchar(15))  returns  varchar(15) deterministic begin  declare  compli_services varchar(5);
if class_id='bussiness' then set compli_services ='yes'; elseif class_id='economy plus' then set compli_services ='yes' ;
else set compli_services ='no'; end if; return compli_services ;end $$ 

delimiter //
create procedure compliment_service() begin select p_date,customer_id,class_id,compli_services(class_id) as compliment_service from ticket_details order by class_id;  end// 
delimiter ; 
call compliment_service();

#Write a query to extract the first record of the customer whose last name ends with Scott using a cursor from the customer table.
delimiter //
create procedure stor_nam() begin declare aa varchar(15); declare bb varchar(15) ;declare cursor_1 cursor for select first_name,last_name FROM customer where last_name like "scott"; open cursor_1; 
repeat fetch cursor_1 into aa , bb ; until bb =0 end repeat ; select aa as first_name , bb as last_name; close cursor_1; end; end // 
delimiter ; 
call stor_nam();
