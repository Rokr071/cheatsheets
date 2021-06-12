
#### **PostgreSQL commands -** 
* Check the version
    ```
    sudo -u postgres psql -c "SELECT version();"
    ```

* To log in to the PostgreSQL server as the postgres user,
 first switch to the user and then access the PostgreSQL 
 prompt using the psql utility;
 The installation procedure created a user account called 
 postgres that is associated with the default Postgres role.
 Switch over to the postgres account on wer server by typing:
   ```
   sudo -i -u postgres
   ```

* we can now access the PostgreSQL prompt immediately by typing:
  ```
  psql 
  ```

* Exit out of the PostgreSQL prompt by typing:
  ```
  \q
  ```

* Accessing a Postgres Prompt Without Switching Accounts
  ```
  sudo -u postgres psql  
  ```

##### Creating a New Role 
  The ```--interactive``` flag will prompt we for the name of the new role and also ask whether it should have superuser permissions.

* If we are logged in as the postgres account, we can create a new user by typing: 
  ```
  createuser --interactive  
  ```


* If, instead, we prefer to use sudo for each command without switching from wer normal account, type:
  ```
  sudo -u postgres createuser --interactive  
  ```

note - We can get more control by passing some additional flags. Check out the options by looking at the manual page:
  ```
  man createuser  
  ```

##### Creating a New Database
  Another assumption that the Postgres authentication system makes by default is that for any role used to log in, that role will have a database with the same name which it can access.

  This means that if the user we created in the last section is called sammy, that role will attempt to connect to a database which is also called “sammy” by default. we can create the appropriate database with the ```createdb``` command.

* If we are logged in as the postgres account, we would type something like:
  ```
  createdb db-name
  ```

* If, instead, we prefer to use sudo for each command without switching from wer normal account, we would type:
  ```
  sudo -u postgres createdb db-name
  ```

##### Opening a Postgres Prompt with the New Role

* If we don’t have a matching Linux user available, we can create one with the ```adduser``` command. we will have to do this from wer non-root account with ```sudo``` privileges (meaning, not logged in as the postgres user):
  ```
  sudo adduser user-name
  ```

* Once this new account is available, we can either switch over and connect to the database by typing:
  ```
  sudo -i -u user-name
  ```
  ```
  psql
  ```

* Or, we can do this inline:
  ```
  sudo -u user-name psql
  ```

* If we want our user to connect to a different database, we can do so by specifying the database like this:
  ```
  psql -d database-name
  ```

* Once logged in, we can get check our current connection information by typing:
  ```
  \conninfo
  ```

##### Creating and Deleting Tables

* The basic syntax for creating tables is as follows:
  ```
  CREATE TABLE table_name (
    column_name1 col_type (field_length) column_constraints,
    column_name2 col_type (field_length),
    column_name3 col_type (field_length)
  );
  ```

* For demonstration purposes, create the following table: 
  ```
  CREATE TABLE playground (
    equip_id serial PRIMARY KEY,
    type varchar (50) NOT NULL,
    color varchar (25) NOT NULL,
    location varchar(25) check (location in ('north', 'south', 'west', 'east', 'northeast', 'southeast', 'southwest', 'northwest')),
    install_date date
  );
  ```

  This command will create a table that inventories playground equipment. The first column in the table will hold equipment ID numbers of the ```serial``` type, which is an auto-incrementing integer. This column also has the constraint of ```PRIMARY KEY``` which means that the values within it must be unique and not null.

  The next two lines create columns for the equipment ```type``` and ```color``` respectively, neither of which can be empty. The line after these creates a ```location``` column as well as a constraint that requires the value to be one of eight possible values. The last line creates a ```date``` column that records the date on which we installed the equipment.

  For two of the columns (```equip_id``` and ```install_date```), the command doesn’t specify a field length. The reason for this is that some data types don’t require a set length because the length or format is implied.

* we can see our new table by typing:
  ```
  \d
  ```

  output -
  ```
                     List of relations
   Schema |          Name           |   Type   |  Owner   
  --------+-------------------------+----------+----------
   public | playground              | table    | postgres
   public | playground_equip_id_seq | sequence | postgres
  (2 rows)
  ```

  our playground table is here, but there’s also something called ```playground_equip_id_seq``` that is of the type ```sequence```. This is a representation of the ```serial``` type which we gave our ```equip_id``` column. This keeps track of the next number in the sequence and is created automatically for columns of this type.

* If we want to see just the table without the sequence, we can type:
  ```
  \dt
  ```

  output -
  ```
             List of relations
   Schema |    Name    | Type  |  Owner   
  --------+------------+-------+----------
   public | playground | table | postgres
  (1 row)
  ```

##### Adding, Querying, and Deleting Data in a Table
* Now that we have a table, we can insert some data into it.
  ```
  INSERT INTO playground (type, color, location, install_date) VALUES ('slide', 'blue', 'south', '2017-04-28');
  ```
  ```
  INSERT INTO playground (type, color, location, install_date) VALUES ('swing', 'yellow', 'northwest', '2018-08-16');
  ```

  note - Do not wrap the column names in quotation marks, but the column values that we enter do need quotes.
  Another thing to keep in mind is that we do not enter a value for the ```equip_id``` column. This is because this is automatically generated whenever we add a new row to the table.

* Retrieve the information we’ve added by typing:
  ```
  SELECT * FROM table-name;
  ```
  example -
  ```
  SELECT * FROM playground;
  ```

  output - 
  ```
    equip_id | type  | color  | location  | install_date 
   ----------+-------+--------+-----------+--------------
           1 | slide | blue   | south     | 2017-04-28
           2 | swing | yellow | northwest | 2018-08-16
   (2 rows)
  ```

  Here, we can see that our ```equip_id``` has been filled in successfully.

* We can also remove the row from our table by typing:
  ```
  DELETE FROM playground WHERE type = 'slide';
  ```
