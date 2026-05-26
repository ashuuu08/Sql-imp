# Sql-imp


# SQL Interview Questions - 40 Important Queries

A comprehensive guide to commonly asked SQL queries in technical interviews. These questions cover basic to advanced topics with practical examples.

---

## Table of Contents
1. [Basic SELECT Queries](#basic-select-queries)
2. [WHERE and Filtering](#where-and-filtering)
3. [JOIN Operations](#join-operations)
4. [Aggregation and Grouping](#aggregation-and-grouping)
5. [Subqueries and Advanced](#subqueries-and-advanced)
6. [Window Functions](#window-functions)
7. [Data Modification](#data-modification)

---

## Basic SELECT Queries

### 1. Simple SELECT Query
**Question:** Write a query to get all columns from the Employees table.
```sql
SELECT * FROM Employees;
```

### 2. SELECT Specific Columns
**Question:** Get employee names and their salaries from the Employees table.
```sql
SELECT EmployeeName, Salary FROM Employees;
```

### 3. SELECT with DISTINCT
**Question:** Get all unique job titles from the Employees table.
```sql
SELECT DISTINCT JobTitle FROM Employees;
```

### 4. SELECT with LIMIT
**Question:** Get the first 10 employees from the Employees table.
```sql
SELECT * FROM Employees LIMIT 10;
```

### 5. SELECT with ORDER BY
**Question:** Get employees sorted by salary in descending order.
```sql
SELECT EmployeeName, Salary FROM Employees ORDER BY Salary DESC;
```

### 6. SELECT with Multiple ORDER BY
**Question:** Get employees sorted by department first, then by salary.
```sql
SELECT * FROM Employees ORDER BY Department, Salary DESC;
```

---

## WHERE and Filtering

### 7. Simple WHERE Clause
**Question:** Get all employees with salary greater than 50000.
```sql
SELECT * FROM Employees WHERE Salary > 50000;
```

### 8. WHERE with AND Operator
**Question:** Get employees from IT department with salary > 60000.
```sql
SELECT * FROM Employees WHERE Department = 'IT' AND Salary > 60000;
```

### 9. WHERE with OR Operator
**Question:** Get employees from IT or HR departments.
```sql
SELECT * FROM Employees WHERE Department = 'IT' OR Department = 'HR';
```

### 10. WHERE with IN Operator
**Question:** Get employees from IT, HR, or Finance departments.
```sql
SELECT * FROM Employees WHERE Department IN ('IT', 'HR', 'Finance');
```

### 11. WHERE with LIKE Operator
**Question:** Get employees whose names start with 'A'.
```sql
SELECT * FROM Employees WHERE EmployeeName LIKE 'A%';
```

### 12. WHERE with BETWEEN
**Question:** Get employees with salary between 40000 and 80000.
```sql
SELECT * FROM Employees WHERE Salary BETWEEN 40000 AND 80000;
```

### 13. WHERE with NULL Check
**Question:** Get all employees without a commission.
```sql
SELECT * FROM Employees WHERE Commission IS NULL;
```

---

## JOIN Operations

### 14. INNER JOIN
**Question:** Get employee names along with their department names.
```sql
SELECT e.EmployeeName, d.DepartmentName 
FROM Employees e 
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```

### 15. LEFT JOIN
**Question:** Get all employees and their projects (if assigned).
```sql
SELECT e.EmployeeName, p.ProjectName 
FROM Employees e 
LEFT JOIN Projects p ON e.EmployeeID = p.AssignedToID;
```

### 16. RIGHT JOIN
**Question:** Get all projects and their assigned employees.
```sql
SELECT p.ProjectName, e.EmployeeName 
FROM Employees e 
RIGHT JOIN Projects p ON e.EmployeeID = p.AssignedToID;
```

### 17. FULL OUTER JOIN
**Question:** Get all employees and projects with all matching records.
```sql
SELECT e.EmployeeName, p.ProjectName 
FROM Employees e 
FULL OUTER JOIN Projects p ON e.EmployeeID = p.AssignedToID;
```

### 18. CROSS JOIN
**Question:** Get all possible combinations of employees and projects.
```sql
SELECT e.EmployeeName, p.ProjectName 
FROM Employees e 
CROSS JOIN Projects p;
```

### 19. Multiple JOINs
**Question:** Get employee name, department, and project information.
```sql
SELECT e.EmployeeName, d.DepartmentName, p.ProjectName 
FROM Employees e 
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID 
LEFT JOIN Projects p ON e.EmployeeID = p.AssignedToID;
```

---

## Aggregation and Grouping

### 20. COUNT Function
**Question:** Count the total number of employees.
```sql
SELECT COUNT(*) as TotalEmployees FROM Employees;
```

### 21. SUM Function
**Question:** Get total salary spent on all employees.
```sql
SELECT SUM(Salary) as TotalSalary FROM Employees;
```

### 22. AVG Function
**Question:** Get average salary of all employees.
```sql
SELECT AVG(Salary) as AverageSalary FROM Employees;
```

### 23. MAX and MIN Functions
**Question:** Get the highest and lowest salary.
```sql
SELECT MAX(Salary) as HighestSalary, MIN(Salary) as LowestSalary FROM Employees;
```

### 24. GROUP BY Simple
**Question:** Get total salary by department.
```sql
SELECT Department, SUM(Salary) as DepartmentSalary 
FROM Employees 
GROUP BY Department;
```

### 25. GROUP BY with COUNT
**Question:** Count employees in each department.
```sql
SELECT Department, COUNT(*) as EmployeeCount 
FROM Employees 
GROUP BY Department 
ORDER BY EmployeeCount DESC;
```

### 26. HAVING Clause
**Question:** Get departments with more than 5 employees.
```sql
SELECT Department, COUNT(*) as EmployeeCount 
FROM Employees 
GROUP BY Department 
HAVING COUNT(*) > 5;
```

### 27. GROUP BY Multiple Columns
**Question:** Get salary by department and job title.
```sql
SELECT Department, JobTitle, COUNT(*) as Count, AVG(Salary) as AvgSalary 
FROM Employees 
GROUP BY Department, JobTitle;
```

---

## Subqueries and Advanced

### 28. Simple Subquery
**Question:** Get employees with salary higher than the average.
```sql
SELECT * FROM Employees 
WHERE Salary > (SELECT AVG(Salary) FROM Employees);
```

### 29. Subquery with IN
**Question:** Get employees who work on projects.
```sql
SELECT * FROM Employees 
WHERE EmployeeID IN (SELECT DISTINCT AssignedToID FROM Projects);
```

### 30. Subquery with EXISTS
**Question:** Get departments that have employees.
```sql
SELECT * FROM Departments d 
WHERE EXISTS (SELECT 1 FROM Employees e WHERE e.DepartmentID = d.DepartmentID);
```

### 31. Correlated Subquery
**Question:** Get employees earning more than their department average.
```sql
SELECT * FROM Employees e1 
WHERE Salary > (SELECT AVG(Salary) FROM Employees e2 
                WHERE e2.Department = e1.Department);
```

### 32. UNION Operator
**Question:** Combine results from two different tables.
```sql
SELECT EmployeeName FROM Employees 
UNION 
SELECT ManagerName FROM Managers;
```

### 33. UNION ALL
**Question:** Combine all records including duplicates.
```sql
SELECT EmployeeName FROM Employees 
UNION ALL 
SELECT ManagerName FROM Managers;
```

### 34. CASE Statement
**Question:** Categorize employees by salary ranges.
```sql
SELECT EmployeeName, Salary,
  CASE 
    WHEN Salary >= 80000 THEN 'High'
    WHEN Salary >= 50000 THEN 'Medium'
    ELSE 'Low'
  END as SalaryRange
FROM Employees;
```

---

## Window Functions

### 35. ROW_NUMBER()
**Question:** Rank employees by salary within each department.
```sql
SELECT EmployeeName, Department, Salary,
  ROW_NUMBER() OVER (PARTITION BY Department ORDER BY Salary DESC) as Rank
FROM Employees;
```

### 36. RANK() and DENSE_RANK()
**Question:** Get ranking with handling of ties.
```sql
SELECT EmployeeName, Salary,
  RANK() OVER (ORDER BY Salary DESC) as Rank,
  DENSE_RANK() OVER (ORDER BY Salary DESC) as DenseRank
FROM Employees;
```

### 37. LAG and LEAD Functions
**Question:** Get current and previous employee salaries when sorted.
```sql
SELECT EmployeeName, Salary,
  LAG(Salary) OVER (ORDER BY HireDate) as PreviousSalary,
  LEAD(Salary) OVER (ORDER BY HireDate) as NextSalary
FROM Employees;
```

### 38. SUM() as Window Function
**Question:** Get running total of salary.
```sql
SELECT EmployeeName, Salary,
  SUM(Salary) OVER (ORDER BY HireDate) as RunningTotal
FROM Employees;
```

---

## Data Modification

### 39. INSERT Query
**Question:** Insert a new employee record.
```sql
INSERT INTO Employees (EmployeeName, Department, Salary, HireDate)
VALUES ('John Doe', 'IT', 75000, '2024-01-15');
```

### 40. UPDATE Query
**Question:** Update salary of employees in IT department.
```sql
UPDATE Employees 
SET Salary = Salary * 1.10 
WHERE Department = 'IT';
```

### Bonus: DELETE Query
**Question:** Delete employees with null commission.
```sql
DELETE FROM Employees 
WHERE Commission IS NULL;
```

---

## Key Concepts to Remember

### Performance Tips
- Always use JOINs instead of multiple queries
- Index frequently searched columns
- Use EXPLAIN to understand query execution
- Avoid SELECT * in production queries

### Best Practices
- Use meaningful aliases for tables
- Write readable and properly formatted SQL
- Add WHERE clauses to limit data processed
- Use appropriate data types
- Avoid using functions on indexed columns in WHERE clauses

### Common Interview Questions About These Queries
1. What's the difference between INNER JOIN and OUTER JOIN?
2. When would you use a subquery vs a JOIN?
3. What's the difference between WHERE and HAVING?
4. Explain the difference between UNION and UNION ALL
5. When should you use window functions?

---

## Practice Database Schema

```sql
-- Employees Table
CREATE TABLE Employees (
  EmployeeID INT PRIMARY KEY,
  EmployeeName VARCHAR(100),
  Department VARCHAR(50),
  Salary DECIMAL(10, 2),
  HireDate DATE,
  Commission DECIMAL(10, 2),
  DepartmentID INT,
  FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);

-- Departments Table
CREATE TABLE Departments (
  DepartmentID INT PRIMARY KEY,
  DepartmentName VARCHAR(50)
);

-- Projects Table
CREATE TABLE Projects (
  ProjectID INT PRIMARY KEY,
  ProjectName VARCHAR(100),
  AssignedToID INT,
  FOREIGN KEY (AssignedToID) REFERENCES Employees(EmployeeID)
);
```

---

## Additional Resources

- Practice regularly on platforms like LeetCode, HackerRank, or Mode Analytics
- Understand EXPLAIN plans for query optimization
- Learn database-specific syntax (MySQL, PostgreSQL, SQL Server, Oracle)
- Study normalization and database design concepts

---

**Last Updated:** 2024
**Difficulty Level:** Beginner to Intermediate
