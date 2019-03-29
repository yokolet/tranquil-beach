# Employees Earning More Than Their Managers

#### Description
- Data Example

```
Table: Employee
+----+-------+--------+-----------+
| Id | Name  | Salary | ManagerId |
+----+-------+--------+-----------+
| 1  | Joe   | 70000  | 3         |
| 2  | Henry | 80000  | 4         |
| 3  | Sam   | 60000  | NULL      |
| 4  | Max   | 90000  | NULL      |
+----+-------+--------+-----------+
```

- Problem

Given the Employee table, write a SQL query that finds out employees who earn more than their managers.

The result of the example above:

```
+----------+
| Employee |
+----------+
| Joe      |
+----------+
```

#### Solution

```sql
SELECT a.Name as Employee
FROM Employee as a, Employee as b
WHERE a.Salary > b.Salary AND a.ManagerId = b.Id;
```