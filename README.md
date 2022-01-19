SQL Task & Stretch Goal - Jonathan White

#Creating database for teams task
CREATE DATABASE OnlineShop;
USE OnlineShop;

#Creating Tables
##creating users table
CREATE TABLE users (
UserID INT auto_increment,
FirstName varchar(100) Not Null,
LastName varchar(100) Not Null,
Email varchar(100) Not Null,
Password varchar(100) Not Null,
DeliveryAddress varchar(100) Not Null,
primary key (UserID)
);

##creating products table
CREATE TABLE products (
ProductID INT auto_increment,
ProductName varchar(100) Not Null,
Price Dec(5,2) Not Null,
primary key (ProductID)
);

##creating orders table
CREATE TABLE orders (
OrderID INT auto_increment,
UserID INT Not Null,
primary key (OrderID),
Foreign key (UserID) references users(UserID)
);

##creating orderline table
CREATE TABLE orderline (
OrderlineID INT auto_increment,
OrderID INT Not Null,
ProductID INT Not Null,
primary key (OrderlineID),
Foreign key (OrderID) references orders(OrderID),
Foreign key (ProductID) references products(ProductID)
);

#Inserting data
##data for Users table
INSERT INTO users (FirstName, LastName, Email, Password, DeliveryAddress) 
values ('Jonathan', 'White', 'jj@test.com', 'Test123', '123 teststreet');
INSERT INTO users (FirstName, LastName, Email, Password, DeliveryAddress) 
values ('JJ', 'Whizzle', 'jj2@test.com', 'P455w0rd', '21 Jump Street'),  ('Jon', 'Jacob-Jinglehimerschmidt', 'jj3@test.com', 'qwerty', '22 Jump Street');
INSERT INTO users (FirstName, LastName, Email, Password, DeliveryAddress) 
values ('Jouson', 'Whit', 'jj4@test.com', 'P455w0rd', '23 Jump Street'),  ('Free', 'Guy', 'RR@sql.com', 'asdfg', 'LA');
Select * FROM users;

##data for products table
INSERT INTO Products (ProductName, Price) 
values ('PS5', '499.99');
INSERT INTO Products (ProductName, Price) 
values ('PS5 - controller', '49.99'),  ('Monitor', '99.99');
INSERT INTO Products (ProductName, Price) 
values ('Kettle', '9.99'),  ('Microwave', '54.45');
Select * FROM products;

##data for orders table
INSERT INTO orders (UserID) Values (1),(2),(4),(3),(5);
Select * FROM orders;

##Data for orderline table
INSERT INTO orderline (OrderID, ProductID) Values (1,1),(2,4),(3,3),(4,5),(5,2);
Select * FROM orderline;

#10 Queries
##1 shows user table contents
Select * FROM users;

##2 shows products table contents
Select * FROM products;

##3 shows order table contents
Select * FROM orders;

##4 nested querie
Select firstname, lastname, email FROM users WHERE userid = (Select userid FROM orders where orderid = 2);

##5 find all names that start with j
Select * FROM users WHERE FirstName Like 'J%';

##6 order delivery address desc and limit 2
Select * FROM users WHERE DeliveryAddress Like '%t' ORDER BY DeliveryAddress DESC LIMIT 2;

##7 join users to orders table
Select * FROM Users JOIN orders ON Users.userid = orders.userid;

##8 double join on orderline table bringing orders and products
Select * FROM orderline Join products ON products.productID = orderline.productID Join orders ON orders.orderID = orderline.orderID; 

##9 Triple Join bringing all tables
Select * FROM orderline Join products ON products.productID = orderline.productID 
Join orders ON orders.orderID = orderline.orderID 
JOIN users ON Users.UserID = Orders.userID;

##10 Organising table to read easier
Select users.UserID, products.ProductName, products.Price, users.FirstName, users.LastName, users.Email, users.Password, users.DeliveryAddress FROM orderline Join products ON products.productID = orderline.productID 
Join orders ON orders.orderID = orderline.orderID 
JOIN users ON Users.UserID = Orders.userID Order by users.userid;

#Deleting rows
##deleting from orderline deleted userid 5 and product kettle
Select * FROM orderline;
set SQL_Safe_updates =0;
DELETE FROM orderline WHERE productID = 4;
DELETE FROM orderline WHERE orderID = 5;
Select * FROM products;

##deleting from products kettle
Select * FROM products;
DELETE FROM products WHERE productID = 4;
Select * FROM products;

##deleting from orders id no.5
Select * FROM orders;
DELETE FROM orders WHERE UserID = 5;
Select * FROM orders;

##deleting from users id no.5
Select * FROM users;
DELETE FROM users WHERE userid = 5;
Select * FROM users;
set SQL_Safe_updates =1;

#Stretch Goal
##creating table
CREATE TABLE Reviews (
ReviewID INT auto_increment,
UserID INT Not Null,
ProductID INT Not Null,
Review Varchar(100) Not Null,
primary key (ReviewID),
foreign key (userid) references	users(userid),
foreign key (ProductID) references products(ProductID)
);

##inserted some data
Insert INTO reviews (UserID, ProductID, Review) values (1, 1, 'Very good');
Insert INTO reviews (UserID, ProductID, Review) values (3, 3, '5 Star');
SELECT * FROM reviews;

##querie to join all relevant tables and re-name columns
Select users.firstname AS 'First Name', users.lastname AS 'Last Name', 
products.productname AS 'Product Bought', review AS 'Reviews' From reviews 
JOIN users ON users.Userid = reviews.userid 
Join products ON products.productID = reviews.productID;# 19-01-SQL-OnlineShop
19-01 SQL OnlineShop completed &amp; stretch goal, Jonathan White
