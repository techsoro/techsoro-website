---
layout: post
title: Relational database
subtitle: Why relational database?
tags: [MySQL]
comments: true
---

What is Relational Database?
A relational database is a collective set of multiple data sets organized by tables, records and columns. Relational databases establish a well-defined relationship between database tables. Tables communicate and share information, which facilitates data searchability, organization and reporting.
Relational databases use Structured Query Language (SQL), which is a standard user application that provides an easy programming interface for database interaction.
CURD Operations :
First, we need to create Database for storing collection of tables.
To create a database, type the following command. Replace dbname with the name of the database that you want to create:
CREATE DATABASE dbname;
To work with the new database, type the following command. Replace dbname with the name of the database you created :
USE dbname;
You can now work with database.
1. Create table in mysql :
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
The column parameters specify the names of the columns of the table.
The datatype parameter specifies the type of data the column can hold (e.g. varchar, integer, date, etc.).
Example :
The following example creates a table called "Student" that contains five columns: RollNo, LastName, FirstName, Address, and City:
CREATE TABLE Student (
    RollNo int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) 
);
Once table is created,you can add records into table by using INSERT INTO statement.
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
Example :
INSERT INTO Student (RollNo, LastName, FirstName,Address, City)
VALUES (101, 'Poul', 'John',  'Kothrud', 'Pune');
INSERT INTO Student123(RollNo, LastName, FirstName,Address, City)
VALUES (102, 'Kohli', 'Virat', 'Manikbaug', 'Pune');
INSERT INTO Student123(RollNo, LastName, FirstName,Address, City)
VALUES (103, 'Patil', 'Neha',  'Dadar', 'Mumbai');
2. Read records from table :
SQL SELECT command to fetch data from the MySQL table.
SELECT * FROM table_name;
Example :
Select * from Student,
RollNo	LastName	FirstName	Address	City
101	Poul	  	John		Kothrud	Pune
102	Kohli		Virat		Manikbaug	Pune
103	Patil		Neha		Dadar		Mumbai
3. Update Statement
The UPDATE statement is used to modify the existing records in a table.
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
Example :
Update address of student having rollno 101 to Kalyani Nagar
UPDATE Student SET Address='Kalyani Nagar' where RollNo=101;

Select * from Student,
RollNo	LastName	FirstName	Address	City
101	Poul	  	John		Kalyani Nagar	Pune
102	Kohli		Virat		Manikbaug	Pune
103	Patil		Neha		Dadar		Mumbai

4. Delete Statement
The DELETE statement is used to delete existing records in a table.
DELETE FROM table_name WHERE condition;
Example :
Delete record having roll no=101 from student table.
DELETE FROM Student where RollNo=101;

Select * from Student,
RollNo	LastName	FirstName	Address	City
102	Kohli		Virat		Manikbaug	Pune
103	Patil		Neha		Dadar		Mumbai
