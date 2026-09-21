-- Create table books

drop table if exists books;

create table books (
  Book_id int primary key,
  Title varchar(150),
  Author varchar(150),
  Genre varchar(150),
  Published_year int,
  Price numeric(10,2),
  Stock int
);

-- create table customers

drop table if exists customers;

create table customers (
	customer_id int primary key,
	name varchar(150),
	email varchar(150),
	phone varchar(150),
	city varchar(150),
	country varchar(150)
);

-- create table orders;

drop table if exists orders;

create table orders (
	order_id int primary key,
	customer_id int references customers(customer_id),
	book_id int references books(book_id),
	order_date date,
	quantity int,
	total_amount numeric (10,2)
);

select * from books;
select * from customers;
select * from orders;

-- imported CSV data into PostgreSQL using pgAdmin's GUI-based Import/Export Data feature
-- without writing a SQL COPY command

-- perform data cleaning

-- check for missing values (null)

select * from books
where  book_id is null
	or title is null
	or author is null
	or genre is null
	or published_year is null
	or price is null
	or stock is null;

select * from customers
where  customer_id is null
	or name is null
	or email is null
	or phone is null
	or city is null
	or country is null;

select * from customers
where  customer_id is null
	or name is null
	or email is null
	or phone is null
	or city is null
	or country is null;

-- check for duplicate records

select title, author, genre, published_year, price, stock, count(*)
from books
group by title, author, genre, published_year, price, stock
having count(*) >1;

select name, email, phone, city, country, count(*)
from customers
group by name, email, phone, city, country
having count(*) >1;

select customer_id, book_id, order_date, quantity, total_amount, count(*)
from orders
group by customer_id, book_id, order_date, quantity, total_amount
having count(*) >1;

-- check for duplicate ids

select book_id, count(*)
from books
group by book_id
having count(*) >1;

select customer_id, count(*)
from customers
group by customer_id
having count(*) >1;

select order_id, count(*)
from orders
group by order_id
having count(*) >1;


-- 1) Retrieve all books in the "Fiction" genre
select * from books
where genre='Fiction';

-- 2) Find Books published after the year 1950
select * from books
where published_year >1950;

-- 3) List all customers from the Canada
select * from customers
where country='Canada';

-- 4) Show orders placed in November 2023
select * from orders
where order_date between '2023-11-01' and '2023-11-30';

-- 5) Retrieve the total stock of books available
select sum(stock) as total_stock
from books;

-- 6) Find the details of the most expensive book
select * from books
order by price desc
limit 1;

-- 7) Show all the customers who ordered more than 1 quantity of book
select * from orders
where quantity >1;

-- 8) Retrieve all orders where the total amount exceeds $300
select * from orders
where total_amount >300;

-- 9) List all genres available in Books table
select distinct(genre)
from books;

-- 10) Find the book with the lowest stock
select * from books
order by stock
limit 1;

-- 11) Calculate the total revenue generated from all orders
select sum(total_amount) as total_revenue
from orders;

select * from books;
select * from customers;
select * from orders;

-- 12) Retrieve the total number of books sold for each genre
select b.genre, sum(o.quantity) as Total_books_sold
from books b
join orders o on o.book_id = b.book_id
group by b.genre;

-- 13) Find the average price of books in the "Fantasy" genre
select avg(price) as avg_price
from books
where genre = 'Fantasy';

-- 14) List customers name with id who have placed at least 3 orders:
select c.customer_id, c.name, count(o.order_id) as Total_orders
from customers c
join orders o on o.customer_id = c.customer_id
group by c.customer_id, c.name
having count(o.order_id) >=3;

-- 15) Find the most frequently ordered book name with id
select o.book_id, b.title, count(o.order_id) as Order_count
from orders o
join books b on b.book_id = o.book_id
group by o.book_id, b.title
order by order_count desc
limit 1;

-- 16) Show the top 3 most expensive books of 'Fantasy' Genre
select * from books
where genre = 'Fantasy'
order by price desc
limit 3;

-- 17) Retrieve the total quantity of books sold by each author
select b.author, sum(quantity) as Total_book_sold
from books b
join orders o on b.book_id = o.book_id
group by author;

-- 18) List the cities where customers who spent over $400
select c.city, o.total_amount
from customers c
join orders o on c.customer_id = o.customer_id
where total_amount >400;

-- 19) Find the customer who spent the most on orders
select c.customer_id, c.name, sum(o.total_amount) as Total_spent
from customers c
join orders o on c.customer_id = o.customer_id
group by c.customer_id, c.name
order by Total_spent desc
limit 1;

-- 20) Calculate the stock remaining after fulfilling all orders
select b.title, b.stock, coalesce(sum(o.quantity),0) as Order_quantity,
b.stock - coalesce(sum(o.quantity),0) as remaining_quantity
from books b
left join orders o on b.book_id = o.book_id
group by b.book_id
order by b.book_id;

-- 21) List the customers with customer id who placed orders with a quantity greater than 5
select c.customer_id, c.name, o.quantity
from orders o
join customers c on o.customer_id = c.customer_id
where o.quantity >5;



















































