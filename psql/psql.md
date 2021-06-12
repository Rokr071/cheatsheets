
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