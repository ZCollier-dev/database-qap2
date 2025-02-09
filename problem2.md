Table Creation:

Create Products Table:

CREATE TABLE products (
id SERIAL PRIMARY KEY,
product_name TEXT,
price DECIMAL(10, 2),
stock_quantity INT
)

Create Customer Table:

CREATE TABLE customers (
id SERIAL PRIMARY KEY,
first_name TEXT,
last_name TEXT,
email TEXT
)

Create Orders Table:

CREATE TABLE orders (
id SERIAL PRIMARY KEY,
customer_id INT REFERENCES customers(id),
order_date DATE
)

Create Order Items Table:

CREATE TABLE order_items (
order_id INT REFERENCES orders(id),
product_id INT REFERENCES products(id),
quantity INT,
PRIMARY KEY (order_id, product_id)
)

Entry Insertion:

Insert data into products table:

INSERT INTO products (product_name, price, stock_quantity)
VALUES
('AAA Batteries', 3.95, 31),
('AA Batteries', 5.95, 16),
('Zip Ties', 6.95, 10),
('Superglue', 7.50, 11),
('Duct Tape', 6.95, 4)

Insert data into customers table:

INSERT INTO customers (first_name, last_name, email)
VALUES
('Miranda', 'Willmott', 'mirandawillmott@gmail.com'),
('Chelsea', 'Brown', 'chelseabrown@hotmail.com'),
('Miranda', 'Elliot', 'mirandaelliot@protonmail.com'),
('Helen', 'Drew', 'helendrew@yahoo.ca')

Insert data into orders table:

INSERT INTO orders (customer_id, order_date)
VALUES
(1, '2024-10-13'),
(2, '2024-10-15'),
(3, '2024-10-20'),
(4, '2024-10-28'),
(1, '2024-11-03')

Insert data into order items table:

INSERT INTO order_items (order_id, product_id, quantity)
VALUES
(1, 1, 3),
(1, 2, 2),
(2, 3, 5),
(2, 5, 2),
(3, 2, 1),
(3, 4, 1),
(4, 3, 2),
(4, 4, 1),
(5, 1, 6),
(5, 5, 1)

Querying:
