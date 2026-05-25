# CRUD Operations
## Insert [Create]
```sql
-- Ensure users table exist
INSERT INTO users (name, email) 
-- name, email are columns
VALUES 
    ('Charlie', 'charlie@example.com'),
    ('Diana', 'diana@example.com'),
    ('Evan', 'evan@example.com');
```

### Note
- For foreign key, references are there
- creating db => connecting => creating table => inserting values => showing to users
```sql
CREATE DATABASE college;

\c college;

CREATE TABLE departments(
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL
);

CREATE TABLE users(
    id          SERIAL PRIMARY KEY,
    name        VARCHAR(100) NOT NULL,
    email       VARCHAR(150) UNIQUE NOT NULL,
    role        VARCHAR(150) NOT NULL CHECK (role IN ('student', 'professor', 'admin')),
    department_id INT REFERENCES departments(id) ON DELETE SET NULL,
    metadata     JSONB,
    is_active    BOOLEAN DEFAULT TRUE,
    created_at   TIMESTAMP DEFAULT now()
);


INSERT INTO departments (id, name) values (1, 'Maths');

SELECT * FROM departments;
```
### Note
- For inserting multiple at once
- If same id is provided It creates conflict
```sql
INSERT INTO departments (id, name) values(2, 'Physics'),(3, 'Chemistry'),(4, 'Biology')
ON conflict (name) do nothing;
-- ignores duplicate names also removes conflict 

select * from departments;
```
Importing from CSV files
```sql
\copy departments(id, name) FROM '/absolute/path/to/departments.csv' WITH DELIMITER ',' CSV HEADER;
```


## Select [Read]
It asks the database a question (query) and fetches specific data from your tables.
\
```*``` It is for everything.
```sql
SELECT name, email, role from users;
SELECT name AS "Full Name", created_at AS "Joined On",role as Profession from users;

SELECT DISTINCT role FROM users; -- It query unique roles
SELECT * FROM users where role = 'professor';
SELECT CONCAT('Mr. ', name) AS "Full Name" FROM users;
SELECT 'Profile: ' || role || ' - ' || name AS "User Badge" FROM users;
-- It prints 'Profile: student - Sk Tonyway'
```
### Note

|Quote Type | Purpose | Example| 
| - | - | - |
Single Quote (') | String Literals (Data/values)| 'Hello World' |
| Double Quote  (") | Identifiers (Tables/Columns) | "Users", "First Name"

We can use BODMAS in SELECT statements.