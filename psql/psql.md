
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
 Switch over to the postgres account on your server by typing:
   ```
   sudo -i -u postgres
   ```

* You can now access the PostgreSQL prompt immediately by typing:
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
  The ```--interactive``` flag will prompt you for the name of the new role and also ask whether it should have superuser permissions.

* If you are logged in as the postgres account, you can create a new user by typing: 
  ```
  createuser --interactive  
  ```


* If, instead, you prefer to use sudo for each command without switching from your normal account, type:
  ```
  sudo -u postgres createuser --interactive  
  ```

note - We can get more control by passing some additional flags. Check out the options by looking at the manual page:
  ```
  man createuser  
  ```