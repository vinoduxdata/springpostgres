# springpostgres

### Prerequisites 
- Java is installed and JAVA_HOME is added in path
- Maven is added and M2_HOME is added in path

Verify by 
``` echo $JAVA_HOME```
```echo $M2_HOME```
Create a "store" DB and seed the data 

In Intellij, maven build tool is configured properly 

### To seed the data 
```brew install postgresql```
```brew services start postgresql```

``psql postgres``
``CREATE DATABASE store;``
\l - to list all the databases
\c store - to connect to store DB 
\dt - to list all the tables of the store DB 
\d products - to describe the table structure 

And then copy and paste the SQL commands inside seed folder 1 by 1 

verify data is seeded by 

```select * from products;```

If it returns nothing, try select count(*) from products.
If that returns 5, Row security: enabled, that’s your culprit.

```SELECT relrowsecurity, relforcerowsecurity
FROM pg_class
WHERE relname = 'store';```

If you see Row security: enabled, that’s your culprit.

```ALTER TABLE store DISABLE ROW LEVEL SECURITY;```

Now, try ```select * from products``` again 

It should return all 5 rows!


