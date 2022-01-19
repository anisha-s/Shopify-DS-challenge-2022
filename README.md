# Shopify-Data Science-Intern-Challenge-2022

* Question 1
~ Given some sample data, write a program to answer the following: click here to access the required data set
~ On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. What metric would you report for this dataset? What is its value?

* Solution:
No of orders: 5000
Total Value of orders: $ 15725640
Total No of Items Sold : 43936

Curently AOV is caluculated as   AOV = Total Value of Orders divide by No of Orders
                                     = 15725640 / 5000
                                     = $ 3145.13
As the quantity per order can be more then one so the correct way to calculate AOV will be
total Value of Orders / Total no. of Items  = 15725640 / 43936 = $357.92
which looks resonable. 


order_id	shop_id	user_id	order_amount	total_items	payment_method	created_at
4716		    78	   818	    77175		         3		      debit		     05-03-2017 05:10
4585		    78	   997	    25725		         1		      cash		     25-03-2017 21:48
4506		    78	   866	    25725		         1		      debit		     22-03-2017 22:06
4421		    78	   969	    77175		         3		      debit		     09-03-2017 15:21
4413		    78	   756	    51450		         2		      debit		     02-03-2017 04:13
4312		    78	   960	    51450		         2		      debit		     01-03-2017 03:02
4193		    78	   787	    77175		         3		      credit_card	 18-03-2017 09:25
4080		    78	   946	    51450		         2		      cash		     20-03-2017 21:14
4041		    78	   852	    25725		         1		      cash		     02-03-2017 14:31
3781		    78	   889	    25725		         1		      cash		     11-03-2017 21:14


These records shown above are the outliners, 19 items are sold at total price of $ 488775
at an average price of 488775/ 19 = 25725
which looks outlandish and all are sold from SHOP_ID of 78


* Question 2
~ For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

** a) How many orders were shipped by Speedy Express in total?
select count(*) from Shippers a ,Orders  b where Shippername = 'Speedy Express' and a.ShipperID = b.ShipperID;

** b)What is the last name of the employee with the most orders?
select b.Lastname,count(a.EmployeeId) from Orders a,Employees b
where a.EmployeeId=b.EmployeeId group by b.EmployeeId,b.Lastname 
ORDER BY count(a.EmployeeId) DESC
LIMIT 1;

** c)What product was ordered the most by customers in Germany?
select b.ProductID, b.ProductName,sum(a.Quantity) as orderqty from OrderDetails a,Products b, Customers c, Orders d
where a.ProductID=b.ProductID and d.OrderID = a.OrderID and d.CustomerID=c.CustomerID
and c.Country='Germany'
group by b.ProductId,b.Productname 
ORDER BY orderqty DESC
LIMIT 1;
