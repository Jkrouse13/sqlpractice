# sqlpractice
How many users are there?  
  `SELECT COUNT (*) FROM users;`

What are the 5 most expensive items?
  `SELECT title, price FROM items ORDER BY price DESC LIMIT 5;`

What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
  `SELECT title, price  FROM items WHERE category = "Books" ORDER BY price LIMIT 1;`
  `or SELECT title, price  FROM items WHERE category LIKE  "%Book%" ORDER BY price LIMIT 1;`


Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
  `SELECT * FROM users INNER JOIN addresses ON users.id = addresses.user_id WHERE addresses.street = "6439 Zetta Hills" AND addresses.city = "Willmouth" AND addresses.state = "WY";`
  `SELECT * FROM addresses INNER JOIN users on addresses.user_id = users.id WHERE users.id ="40";`
  They have two addresses.

Correct Virginie Mitchell's address to "New York, NY, 10108".
  `SELECT * FROM users WHERE users.first_name = "Virginie" AND users.last_name = "Mitchell";`
  `UPDATE addresses SET city = "New York", state = "NY", zip = "10108" WHERE user_id = "39";`

How much would it cost to buy one of each tool?
  `SELECT SUM(price) FROM items WHERE category LIKE "%Tools%";`

How many total items did we sell?
  `SELECT SUM(quantity) FROM orders;`

How much was spent on books?
  `SELECT SUM(items.price * orders.quantity) FROM items INNER JOIN orders  ON (items.id = orders.item_id) WHERE category LIKE "%Books%";`

Simulate buying an item by inserting a User for yourself and an Order for that User.
  `INSERT INTO users (first_name, last_name, email) VALUES ("Jon", "Krouse", "jk@haha.net");`
  `INSERT INTO orders (user_id, item_id, quantity, created_at) VALUES ("51", "13", "89", date('now'));`
