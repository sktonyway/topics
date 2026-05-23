# DATABASE CLI operations

### Creating a Database
```sql 
CREATE DATABASE myapp;
```
```sql 
CREATE DATABASE IF NOT EXISTS myapp;
```
### Listing all Databases

```sql 
\l; -- lists all databases
```
```sql 
\l+; -- lists databases in details
```
### Connecting Database
```sql 
\c myapp; -- connecting to myapp database
```

### Dropping Database

```sql 
DROP DATABASE myapp;  -- deleting the database
```

```sql 
DROP DATABASE IF EXISTS myapp;
```

## Key Concepts 
### Table
A structured Container inside database like spreadsheets.
```sql 
\dt; -- to show all tables
```
```sql 
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    HireDate DATE
);
-- create table of employees with these structure
```

```sql 
DROP TABLE Employees; -- remove employees table from database
```
Remeber these before creating a table:
- Don't use trailing commas in creating table.
- Pick consistent naming conventions in casing, singular-plural etc.
- Don't over-allocate VARCHAR [It wastes[] space]
### Column / Field
### Row / Record
### Primary key

```bash
# Using docker container
# starts docker container with name my-postgres
docker run --name my-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres

# open postres container on my bash
docker exec -it my-postgres bash

# starting psql
psql -U postgres

# list all databases
\l 
CREATE DATABASE dummy;
\c dummy;
```
#### Now [CRUD](./crud.md) can be performed using CLI.
