
* Step 1 - Create tables: 

```
CREATE TABLE cricketer_matches (
  player_id int PRIMARY KEY NOT NULL,
  test_matches int NOT NULL CHECK (test_matches >= 0),
  odi_matches int NOT NULL CHECK (odi_matches >= 0),
  t20i_matches int NOT NULL CHECK (t20i_matches >= 0)
);
```

```
CREATE TABLE cricketer_runs (
  player_id int PRIMARY KEY NOT NULL,
  test_runs int NOT NULL CHECK (test_runs >= 0),
  odi_runs int NOT NULL CHECK (odi_runs >= 0),
  t20i_runs int NOT NULL CHECK (t20i_runs >= 0)
);
```

```
CREATE TABLE cricketer_wickets (
  player_id int PRIMARY KEY NOT NULL,
  test_wickets int NOT NULL CHECK (test_wickets >= 0),
  odi_wickets int NOT NULL CHECK (odi_wickets >= 0),
  t20i_wickets int NOT NULL CHECK (t20i_wickets >= 0)
);
```

```
CREATE TABLE cricketer_top_score (
  player_id int PRIMARY KEY NOT NULL,
  test_top_score int NOT NULL CHECK (test_top_score >= 0),
  odi_top_score int NOT NULL CHECK (odi_top_score >= 0),
  t20i_top_score int NOT NULL CHECK (t20i_top_score >= 0)
);
```

```
CREATE TABLE cricketer_debut_date (
  player_id int PRIMARY KEY NOT NULL,
  test_debut date,
  odi_debut date,
  t20i_debut date
);
```

```
CREATE TABLE cricketers (
  player_id int PRIMARY KEY NOT NULL,
  firstname varchar (50) NOT NULL,
  lastname varchar (25) NOT NULL,
  nation varchar(50) NOT NULL,
  role varchar(50) NOT NULL,
  FOREIGN KEY(player_id) REFERENCES cricketer_matches(player_id),
  FOREIGN KEY(player_id) REFERENCES cricketer_runs(player_id),
  FOREIGN KEY(player_id) REFERENCES cricketer_wickets(player_id),
  FOREIGN KEY(player_id) REFERENCES cricketer_top_score(player_id),
  FOREIGN KEY(player_id) REFERENCES cricketer_debut_date(player_id)
);
```

* Step 2 - Insert data - 

```
INSERT INTO cricketer_matches (player_id, test_matches, odi_matches, t20i_matches) 
VALUES 
(1, 91, 254, 90),
(2, 38, 227, 111),
(3, 84, 151, 67),
(4, 18, 67, 50);
```

```
INSERT INTO cricketer_runs (player_id, test_runs, odi_runs, t20i_runs) 
VALUES
(1, 7490, 12169, 3159),
(2, 2615, 9205, 2864),
(3, 7129, 6173, 1805),
(4, 42, 19, 8);
```

```
INSERT INTO cricketer_wickets (player_id, test_wickets, odi_wickets, t20i_wickets) 
VALUES 
(1, 0, 4, 4),
(2, 2, 8, 1),
(3, 30, 37, 6),
(4, 84, 108, 59);
```

```
INSERT INTO cricketer_top_score (player_id, test_top_score, odi_top_score, t20i_top_score) 
VALUES 
(1, 254, 183, 94),
(2, 212, 264, 118),
(3, 251, 148, 95),
(4, 10, 10, 7);
```

```
INSERT INTO cricketer_debut_date (player_id, test_debut, odi_debut, t20i_debut) 
VALUES 
(1, '2011-06-20', '2008-08-18', '2010-06-12'),
(2, '2013-11-06', '2007-06-23', '2007-09-19'),
(3, '2010-11-04', '2010-08-10', '2011-10-16'),
(4, '2018-01-05', '2016-01-23', '2016-01-26');
```

```
INSERT INTO cricketers (player_id, firstname, lastname, nation, role) 
VALUES 
(1, 'virat', 'kholi', 'india', 'batsman'),
(2, 'rohit', 'sharma', 'india', 'batsman'),
(3, 'kane', 'williamson', 'new zealand', 'batsman'),
(4, 'jasprit', 'bumrah', 'india', 'bowler');
```

* Step 3 - PostgreSQL Joins

- **PostgreSQL Inner Join** -

```
SELECT * FROM table_name_1 INNER JOIN table_name_2 ON table_name_1.some_column_name = table_name_2.some_column_name; 
```

example -

```
SELECT * FROM cricketers INNER JOIN cricketer_matches ON cricketers.player_id = cricketer_matches.player_id; 
```

The inner join examines each row in the first table (cricketers). It compares the value in the fruit_a column with the value in the fruit_b column of each row in the second table (cricketer_matches). If these values are equal, the inner join creates a new row that contains columns from both tables and adds this new row the result set.

![alt text](inner-join.png)