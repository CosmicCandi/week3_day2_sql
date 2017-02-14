# week3_day2_sql
Week 3 - Day 2 - Working with SQLite3

Explorer Mode

How many users are there? 50
`SELECT COUNT(*) FROM users;`

What are the 5 most expensive items?
title|price
Small Cotton Gloves|9984
Small Wooden Computer|9859
Awesome Granite Pants|9790
Sleek Wooden Hat|9390
Ergonomic Steel Car|9341

`SELECT title, price FROM items ORDER BY items.price DESC LIMIT 5;`

What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?) Ergonomic Granite Chair|1496
`SELECT title, price FROM items ORDER BY items.price DESC LIMIT 1;`

Who lives at "6439 Zetta Hills, Willmouth, WY"?
Corinne Little
`SELECT first_name, last_name
FROM users INNER JOIN addresses
ON users.id = addresses.user_id
WHERE street == "6439 Zetta Hills" AND city == "Willmouth" AND state =="WY";`

Do they have another address? Yes. 54369 Wolff Forges, Lake Byron, CA 31587

`SELECT users.first_name, users.last_name,  addresses.street, addresses.city, addresses.state, addresses.zip
FROM users INNER JOIN addresses
ON users.id = addresses.user_id
WHERE users.first_name = "Corrine" AND users.last_name == "Little";`

Correct Virginie Mitchell's address to "New York, NY, 10108". 41|39|12263 Jake Crossing|New York|NY|10108
`UPDATE addresses SET
city = "New York", zip = 10108
WHERE street == "12263 Jake Crossing";`


How much would it cost to buy one of each tool? $46,477

`SELECT SUM(*) FROM items WHERE category LIKE '%Tool%';`

How many total items did we sell? 2125
`SELECT SUM(quantity) FROM orders;`

How much was spent on books? $1,081,352
`SELECT SUM(items.price * orders.quantity)
FROM items INNER JOIN orders ON items.id = orders.item_id
WHERE items.category LIKE '%Book%';`

Simulate buying an item by inserting a User for yourself and an Order for that User. id|user_id|item_id|quantity|created_at
378|51|46|1|2017-02-14 23:02:46
`INSERT INTO users (first_name, last_name, email) VALUES ("Kalea", "Wolff", "kalea.wolff@gmail.com");`

`INSERT INTO orders (user_id, item_id, quantity, created_at)
VALUES (51, 46, 1, CURRENT_TIMESTAMP);`

Adventure Mode
What item was ordered most often? Grossed the most money?
What user spent the most?
What were the top 3 highest grossing categories?

Epic Mode

Complete the exercises on sqlteaching.com as well and add a screenshot of the final screen showing all exercises completed to your README.
