# MYSQL Guide Sheet

This is a **MySQL Guide Sheet** and can be used as basic guidelines for mySQL fundamentals.

## Usage
Follow the guidelines for mySQL in this syntax guide.
- [How to login into mysql from terminal](#how-to-login-into-mysql-from-terminal)
- [How to SHOW USERS](#how-to-show-users)
- [How to CREATE USERS](#how-to-create-users)
- [How to GRANT PRIVILEGES, Show granted privileges and remove.](#how-to-grant-privileges)
- [How to SHOW, DELETE & CREATE DATABASES & SELECT DATABASES](#how-to-show-delete-and-create-databases)
- [How to CREATE a TABLE with Columns and their data types](#how-to-create-a-table-with-columns-and-their-data-types)
- [How to SHOW, DELETE & DROP Tables](#how-to-show-delete-and-drop-tables)
- [How to Insert ROWS & RECORDS (single and multiple)](#how-to-insert-rows-and-records)
- [How to SELECT with the WHERE Clause](#how-to-select-with-the-where-clause)
- [How to SELECT with the WHERE Clause using a range](#how-to-select-with-where-and-range)
- [How to DELETE an individual ROW](#how-to-delete-an-individual-row)
- [How to UPDATE a ROW](#how-to-update-a-row)
- [How to add a new column and modify it)](#how-to-add-a-new-column-and-modify-it)
- [How to Order by and use Distinct](#how-to-order-by-and-use-distinct)
- [How to Concatenate Columns](#how-to-concatenate-columns)
- [How to Select Distinct Rows](#how-to-select-distinct-rows)
- [How to use LIKE to Search](#how-to-use-like)
- [How Select using IN](#how-to-select-using-in)
- [How to Create & Remove Index](#how-to-create-and-remove-index)
- [Create Two Tables demonstrating a one to many relationship that shows a PK & FK](#primary-key-and-foreign-key)
- [How to use Inner Join](#how-to-use-inner-join)
- [How to JOIN Multiple Tables](#how-to-join-multiple-tables)
- [How to tunnel mySQL locally via SSH](#how-to-tunnel-mysql-locally-via-ssh)

## How to login into mysql from terminal
Once locally connected to the server, use:
```console
sudo mysql -u root -p
```

## How to SHOW USERS
Once logged into mysql, it's possible to change to use mysql, then `SELECT user from user;` as shown below:
```sql
use mysql;
SELECT user FROM user;
```

## How to CREATE USERS
It's possible to create users in mysql with the following snippet:
```sql
CREATE USER 'local_new_user'@'localhost' IDENTIFIED BY 'the_pass';

```

## How to GRANT PRIVILEGES
This is how to GRANT PRIVILEGES.
```sql
GRANT ALL PRIVILEGES on the_database.* to 'local_new_user'@'localhost';
```

## How To Show Delete And Create Databases
This is how to show, delete, and create databases. It can also be done via myPhpAdmin.
```sql
# Show databases
SHOW DATABASES;
# Delete the databases
DROP database_name;
# Create the database if it doesn't already exist
CREATE DATABASE IF NOT EXISTS somedatabase;
```

## How to create a table with columns and their data types
This is a snippet example of how to create a table with columns and data types.
```sql
# Example of how to create a table with data type assignment
CREATE TABLE IF NOT EXISTS SomeTable (
  Id INT AUTO_INCREMENT,
  Name varchar(255),
  Username varchar(255) NOT NULL DEFAULT (UUID()) UNIQUE,
  PRIMARY KEY (ID)
);
```

## How to show delete and drop tables
This is how to show, delete and drop tables.
```sql
SHOW TABLES;
# Or full view
SHOW FULL TABLES;
# Drop the table
DROP TABLE SomeTable;
```

## How to insert rows and records
This is how to save new items in the table.
```sql
# Save a book
INSERT INTO Books
(BookName, Genre, Author, Barcode)
VALUES
("somebookname", "somegenre", "someauthor", "somebarcode");
```

## How to select with the where clause
This is how to select specific attributes using WHERE.
```sql
UPDATE Books SET BookName = '$someNewTitle' WHERE BookId = $someBookId;
```

## How to select with where and range
This is how to select with WHERE and using a range.
```sql
SELECT someName, somePrice
FROM items
WHERE somePrice > 15 AND somePrice < 20
```

## How to delete an individual row
Delete an individual row where a specific attribute is present.
```sql
DELETE FROM items WHERE someId=2;
```

## How to update a row
Update an individual row where a specific attribute is present.
```sql
UPDATE Books SET BookName = '$newtitleIn' WHERE BookId = $bookId;
```

## How to add a new column and modify it
Alter a table and add a new column
```sql
ALTER TABLE books
ADD someIdentifier someDataType;
```

## How to order by and use distinct
Order by and distinct examples:
```sql
SELECT * FROM Places
ORDER BY country DESC;
```

## How to concatenate columns
This is how to concat columns in mysql.
```sql
select CONCAT(someColumn, ' ', someColumnTwo) as asVariableName from someTable;
```

## How to select distinct rows
How to select distinct rows.
```sql
SELECT  DISTINCT *
FROM items
WHERE product_type = 'car'
ORDER BY names
LIMIT 10;
```

## How to use LIKE to Search
Using like with a starts with attribute:
```sql
SELECT columnOne, columnTwo
FROM someTable
WHERE smoeColumn LIKE 'startsWith%'
```

## How to select using in
Select with in example:
```sql
SELECT * FROM items
WHERE country IN ('Germany', 'France', 'UK');
```

## How to create and remove index
How to create and remove indexes:
```sql
# Add Index
CREATE INDEX someColumnName
ON Persons (FirstName);
# Remove index
ALTER TABLE someTable
DROP INDEX someIndexName;
```

## Primary key and foreign key
This shows declaring primary and foreign keys.
```sql
CREATE TABLE IF NOT EXISTS BorrowRecord (
	BorrowRecordId INT AUTO_INCREMENT,
    ThisBookId INT NOT NULL,
    PersonBorrowingId INT NOT NULL,
    BorrowingSessionExpiry TIMESTAMP,
    PRIMARY KEY (BorrowRecordId),
    FOREIGN KEY (ThisBookId) REFERENCES Books(BookId),
    FOREIGN KEY (PersonBorrowingId) REFERENCES PersonsBorrowing(Id)
);
```

## How to use inner join
This shows how to use a JOIN
```sql
USE ORG;

SELECT FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT
FROM Worker
INNER JOIN Title
ON Worker.WORKER_ID = Title.WORKER_REF_ID WHERE WORKER_TITLE = "Manager";

```

## How to join multiple tables
This is how to join multiple tables:
```sql
SELECT
  student.first_name,
  student.last_name,
  course.name
FROM student
JOIN student_course
  ON student.id = student_course.student_id
JOIN course
  ON course.id = student_course.course_id;
```

## How to tunnel mysql locally via ssh
This is a way to tunnel mysql locally via ssh for easier local development connecting to a remote ssh server and mysql server port tunneling.
```console
#Connect to the remote host and set the tunnel port to 3306 for mysql default
ssh -Ng -L 3307:127.0.0.1:3306 username@remotehost

#Then set locally a tunnel port to 3307 with the database and username for mysql
mysql -h 127.0.0.1 -P 3307 -u username -p worldDatabase
```