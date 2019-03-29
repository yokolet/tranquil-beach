# Second Highest Salary

#### Description
- Data Example

```
Table: Employee
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

- Problem

Write a SQL query to get the second highest salary from the Employee table. If there is no second highest salary, the query should return null.

The result of the example above:

```
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
```

#### Solution

```sql
SELECT(SELECT DISTINCT Salary
       FROM Employee
       ORDER BY Salary DESC LIMIT 1, 1)
       AS SecondHighestSalary;
```
