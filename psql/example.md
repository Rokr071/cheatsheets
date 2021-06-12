
- **Create Tables -**

	```
	CREATE TABLE cricketers (
 	id int NOT NULL,
 	firstname varchar(50) NOT NULL,
 	lastname varchar(50) NOT NULL,
 	date_of_birth date NOT NULL,
 	country varchar(50) NOT NULL,
 	PRIMARY KEY (id)
	);
	```

 	```
	CREATE TABLE odi_statistics (
    id serial PRIMARY KEY,
    player_id int NOT NULL,
	firstname varchar(50) NOT NULL,
	odi_matches int NOT NULL CHECK(odi_matches >= 0),
	odi_runs int NOT NULL CHECK(odi_runs >= 0),
	odi_wickets int NOT NULL CHECK(odi_wickets >= 0)
	);
	```

- **Insert Data Into Tables -**

	```
	INSERT into cricketers (id, firstname, lastname, date_of_birth, country) 
	VALUES 
	(1, 'virat', 'kholi', '1988-11-05', 'india'),
	(2, 'rohit', 'sharma', '1987-04-30', 'india'),
	(3, 'kane', 'williamson', '1990-08-08', 'new zealand');
	```

	```
	INSERT into odi_statistics (player_id, firstname, odi_matches, odi_runs, odi_wickets) 
	VALUES 
	(1, 'virat', 254, 12169, 4),
	(4, 'tim', 35, 890, 0),
	(5, 'joe', 149, 5962, 26);
	```

- **JOINS -**

	- **inner join (i.e. common only) -** 
	```
	SELECT * FROM cricketers INNER JOIN odi_statistics ON cricketers.id = odi_statistics.player_id;
	```

	- **left join -** 
	```
	SELECT * FROM cricketers LEFT JOIN odi_statistics ON cricketers.id = odi_statistics.player_id;
	```

	- **left outer join (i.e. exclusive to left only) -**
	```
	SELECT * FROM cricketers LEFT JOIN odi_statistics ON cricketers.id = odi_statistics.player_id WHERE odi_statistics.player_id IS NULL;
	```
	
		Note that the LEFT JOIN is the same as the LEFT OUTER JOIN so you can use them interchangeably.

	- **right join -** 
	```
	SELECT * FROM cricketers RIGHT JOIN odi_statistics ON cricketers.id = odi_statistics.player_id;
	```

	- **right outer join (i.e. exclusive to right only) -** 
	```
	SELECT * FROM cricketers RIGHT JOIN odi_statistics ON cricketers.id = odi_statistics.player_id WHERE cricketers.id IS NULL;
	```

		Note that the RIGHT JOIN and RIGHT OUTER JOIN are the same therefore you can use them interchangeably.


	- **full outer join (i.e. all) -**
	```
	SELECT * FROM cricketers FULL OUTER JOIN odi_statistics ON cricketers.id = odi_statistics.player_id;
	```
 	
 	- **full join (i.e. non-matching from both) -**
 	```
	SELECT * FROM cricketers FULL JOIN odi_statistics ON cricketers.id = odi_statistics.player_id 
	WHERE cricketers.id IS NULL OR odi_statistics.player_id IS NULL;
	```