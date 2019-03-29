# Combine Two Tables

#### Description

- SQL Schema

```
Table: Person
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
PersonId is the primary key column for this table.

Table: Address
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
AddressId is the primary key column for this table.
```

- Problem

Write a SQL query to show the information below for each person in the Person table, regardless if there is an address for each of those people.

```
FirstName, LastName, City, State
```

#### Solution

```sql
SELECT p.FirstName, p.LastName, a.City, a.State 
FROM Person AS p LEFT JOIN Address AS a ON p.PersonId = a.PersonId;
```