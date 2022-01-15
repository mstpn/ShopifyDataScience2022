# Data Science Challenge for Shopify 2022 Internship

## Question 1: 
Please see the q1.ipynb Jupyter notebook for my program and detailed answers.

A brief summary of my answers: <br>
a) The naive AOV calculation takes the mean of all orders, and there are several orders over $700,000 that skew this mean <br>
b) Median Order Value <br>
c) $284.00 <br>

## Question 2:
q2.txt contains the plain text versions of the answers below. <br>
(Browser used: Firefox)

### a. How many orders were shipped by Speedy Express in total?
```
SELECT COUNT(*) AS SpeedyOrders <br>
FROM Orders, Shippers <br>
WHERE Orders.ShipperID = Shippers.ShipperID AND Shippers.ShipperName = 'Speedy Express'; <br>
```
Answer:
54


### b. What is the last name of the employee with the most orders?
```
SELECT Employees.LastName  <br>
FROM Employees, <br>
	(SELECT Top 1 EmployeeID, COUNT(EmployeeID) AS EmployeeOrders <br>
	FROM Orders <br>
	GROUP BY EmployeeID <br>
	ORDER BY COUNT(EmployeeID) DESC) AS MostOrders <br>
WHERE Employees.EmployeeID = MostOrders.EmployeeID; <br>
```
Answer:
Peacock


### c. What product was ordered the most by customers in Germany?
```
SELECT Products.ProductName
FROM Products,  <br>
  (SELECT Top 1 OrderDetails.ProductID, SUM(OrderDetails.Quantity) AS ProductOccurence <br>
  FROM OrderDetails, Customers, Orders, Products <br>
  WHERE Orders.OrderID = OrderDetails.OrderID <br>
      AND OrderDetails.ProductID = Products.ProductID <br>
      AND Orders.CustomerID = Customers.CustomerID <br>
      AND Customers.Country = 'Germany' <br>
  GROUP BY OrderDetails.ProductID <br>
  ORDER BY SUM(OrderDetails.Quantity) DESC) AS PopularItem <br>
WHERE PopularItem.ProductID = Products.ProductID; <br>
```
Answer:
Boston Crab Meat
