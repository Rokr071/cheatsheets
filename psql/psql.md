
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
