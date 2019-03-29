# Nth Highest Salary

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

Write a SQL query to get the nth highest salary from the Employee table. If there is no nth highest salary, the query should return null.

The result of the example above:

```
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```

#### Solution

```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  SET N = N-1;
  RETURN (
      SELECT DISTINCT(Salary)
      FROM Employee ORDER BY Salary DESC LIMIT N,1
  );
END
```

