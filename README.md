# CTS

-- USERS TABLE STARTS HERE

ALTER TABLE customer
RENAME TO users;

CREATE TABLE users(
 id serial PRIMARY KEY,
 username VARCHAR (50) UNIQUE NOT NULL,
 password VARCHAR (50) NOT NULL,
 email VARCHAR (355) UNIQUE NOT NULL,
 phonenumber BIGINT UNIQUE NOT NULL,
 address TEXT,
 city VARCHAR (50),
 state VARCHAR (50),
 pincode INTEGER,
 created_on TIMESTAMP NOT NULL,
 last_login TIMESTAMP
);

INSERT INTO users(username, password, email, phonenumber, address, city, state, pincode, created_on, last_login)
VALUES ('karthikeyan','Login@12345', 'uiprovider@gmail.com', 8220831050, '5/1333 kumarasamy nagar muthiapuram','Thoothukudi','Tamil Nadu',628005, NOW(), NOW());

UPDATE users SET created_on = NOW();

UPDATE users SET last_login = NOW();

DELETE FROM users
WHERE id=1;

-- USERS TABLE ENDS HERE


-- PRODUCT TABLE STARTS HERE

CREATE TABLE product(
 id serial PRIMARY KEY,
 productname VARCHAR (50) UNIQUE NOT NULL,
 description TEXT,
 created_on TIMESTAMP NOT NULL
);

INSERT INTO product(productname, description, created_on) 
VALUES ('product one', 'product one description', NOW());

UPDATE product SET created_on = NOW();
		
DELETE FROM product
WHERE id=2;		

-- TABLE ENDS HERE


-- TABLE ORDER STARTS HERE

CREATE TABLE orders(
  id serial PRIMARY KEY,
  customer_id integer NOT NULL,
  description TEXT,
  created_on TIMESTAMP NOT NULL,
  FOREIGN KEY (customer_id) REFERENCES users (id)
);

INSERT INTO orders(customer_id, description, created_on) 
VALUES (2, 'product one description', NOW());

UPDATE orders SET created_on = NOW();

DELETE FROM orders
WHERE id=1;
		
-- TABLE ORDER ENDS


-- TABLE ORDER ITEM STARTS HERE

CREATE TABLE orderitem(
  id serial PRIMARY KEY,
  customer_id integer NOT NULL,
  orders_id integer NOT NULL,
  quantity SMALLINT NOT NULL,
  created_on TIMESTAMP NOT NULL,
  FOREIGN KEY (customer_id) REFERENCES users (id),	
  FOREIGN KEY (orders_id) REFERENCES orders (id)
);

INSERT INTO orderitem(customer_id, orders_id, quantity, created_on) 
VALUES (2, 3, 3, NOW());

UPDATE orderitem SET created_on = NOW();

DELETE FROM orderitem
WHERE id=2;
		
-- TABLE ORDER ITEM ENDS HERE


-- TABLE ROLE STARTS HERE

CREATE TABLE role(
 id serial PRIMARY KEY,
 name VARCHAR (255) UNIQUE NOT NULL,
 created_on TIMESTAMP NOT NULL
);

INSERT INTO role(name, created_on) 
VALUES ('USER', NOW());

-- TABLE ROLE ENDS HERE


-- TABLE ACCOUNT_ROLE ENDS HERE
		
CREATE TABLE account_role
(
  user_id integer NOT NULL,
  role_id integer NOT NULL,
  grant_date timestamp without time zone,
  PRIMARY KEY (user_id, role_id),
  FOREIGN KEY (role_id)
      REFERENCES role (id) MATCH SIMPLE
      ON UPDATE NO ACTION ON DELETE NO ACTION,
  FOREIGN KEY (user_id)
      REFERENCES users (id) MATCH SIMPLE
      ON UPDATE NO ACTION ON DELETE NO ACTION
);

INSERT INTO account_role(user_id, role_id, grant_date) 
VALUES (2,1, NOW());
		
DELETE FROM account_role
WHERE user_id=2;		

-- TABLE ACCOUNT_ROLE ENDS HERE
		
		
		
		
