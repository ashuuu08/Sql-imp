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
# SQL Interview Questions & Answers - Complete Guide

A comprehensive guide with 60+ SQL queries, detailed explanations, and important difference-based questions commonly asked in technical interviews.

---

## Table of Contents
1. [Basic Queries with Explanations](#basic-queries-with-explanations)
2. [Intermediate Queries](#intermediate-queries)
3. [Advanced Queries](#advanced-queries)
4. [Difference Between Questions](#difference-between-questions)
5. [Real-World Scenarios](#real-world-scenarios)
6. [Database Schema](#database-schema)

---

## Basic Queries with Explanations

### 1. Simple SELECT Query
**Question:** Write a query to fetch all records from the Employees table.
```sql
SELECT * FROM Employees;
```
**Explanation:** The asterisk (*) retrieves all columns from the table. This is generally avoided in production due to performance concerns.

**When to use:** For exploration and debugging, but not recommended for production queries.

---

### 2. SELECT Specific Columns
**Question:** Get employee IDs, names, and salaries.
```sql
SELECT EmployeeID, EmployeeName, Salary FROM Employees;
```
**Explanation:** Only fetches specified columns, which is more efficient than SELECT *.

**Output Example:**
```
EmployeeID | EmployeeName | Salary
-----------|--------------|--------
1          | John Doe     | 75000
2          | Jane Smith   | 85000
```

---

### 3. SELECT with DISTINCT
**Question:** Find all unique job titles in the company.
```sql
SELECT DISTINCT JobTitle FROM Employees;
```
**Explanation:** DISTINCT removes duplicate values from results.

**Without DISTINCT:** 
```
JobTitle
---------
Manager
Developer
Manager
Developer
Analyst
```

**With DISTINCT:**
```
JobTitle
---------
Manager
Developer
Analyst
```

---

### 4. SELECT with WHERE Clause
**Question:** Get all employees earning more than 60,000.
```sql
SELECT EmployeeName, Salary FROM Employees WHERE Salary > 60000;
```
**Explanation:** WHERE filters rows based on conditions. Only rows satisfying the condition are returned.

---

### 5. SELECT with AND Operator
**Question:** Get employees from IT department earning more than 70,000.
```sql
SELECT * FROM Employees 
WHERE Department = 'IT' AND Salary > 70000;
```
**Explanation:** AND requires all conditions to be true.

**Logic:**
- Condition 1: Department = 'IT' âœ“
- Condition 2: Salary > 70000 âœ“
- Result: Both must be TRUE

---

### 6. SELECT with OR Operator
**Question:** Get employees from IT or HR departments.
```sql
SELECT * FROM Employees 
WHERE Department = 'IT' OR Department = 'HR';
```
**Explanation:** OR requires at least one condition to be true.

---

### 7. SELECT with IN Operator
**Question:** Get employees from IT, HR, and Finance departments.
```sql
SELECT * FROM Employees 
WHERE Department IN ('IT', 'HR', 'Finance');
```
**Explanation:** IN is cleaner than multiple OR statements. Equivalent to:
```sql
WHERE Department = 'IT' OR Department = 'HR' OR Department = 'Finance'
```

---

### 8. SELECT with NOT IN
**Question:** Get all employees NOT from IT or HR.
```sql
SELECT * FROM Employees 
WHERE Department NOT IN ('IT', 'HR');
```
**Explanation:** Returns rows that don't match any value in the list.

---

### 9. SELECT with LIKE (Pattern Matching)
**Question:** Get employees whose names start with 'J'.
```sql
SELECT * FROM Employees WHERE EmployeeName LIKE 'J%';
```
**Explanation:** LIKE uses wildcards:
- `%` = any number of characters
- `_` = single character

**Examples:**
- `'A%'` - Starts with A
- `'%Smith'` - Ends with Smith
- `'J_hn'` - Exactly 4 chars starting with J, ending with hn
- `'%Dev%'` - Contains Dev anywhere

---

### 10. SELECT with BETWEEN
**Question:** Get employees with salaries between 50,000 and 80,000.
```sql
SELECT * FROM Employees 
WHERE Salary BETWEEN 50000 AND 80000;
```
**Explanation:** BETWEEN is inclusive on both ends (>=50000 AND <=80000).

---

### 11. SELECT with IS NULL
**Question:** Get employees who don't have a commission.
```sql
SELECT * FROM Employees WHERE Commission IS NULL;
```
**Explanation:** Use IS NULL to check for NULL values. You cannot use `= NULL`.

---

### 12. SELECT with IS NOT NULL
**Question:** Get employees who have a commission assigned.
```sql
SELECT * FROM Employees WHERE Commission IS NOT NULL;
```
**Explanation:** Returns non-NULL values.

---

### 13. ORDER BY Single Column
**Question:** Get employees sorted by salary (highest to lowest).
```sql
SELECT EmployeeName, Salary FROM Employees 
ORDER BY Salary DESC;
```
**Explanation:**
- `ASC` = Ascending (default, lowest to highest)
- `DESC` = Descending (highest to lowest)

**Output:**
```
EmployeeName | Salary
-------------|--------
Sarah Miller | 95000
Jane Smith   | 85000
John Doe     | 75000
```

---

### 14. ORDER BY Multiple Columns
**Question:** Sort by department (ascending), then by salary (descending) within each department.
```sql
SELECT Department, EmployeeName, Salary FROM Employees 
ORDER BY Department ASC, Salary DESC;
```
**Explanation:** First sorts by Department, then sorts by Salary within each department group.

---

### 15. SELECT with LIMIT
**Question:** Get the top 5 highest-paid employees.
```sql
SELECT TOP 5 EmployeeName, Salary FROM Employees 
ORDER BY Salary DESC;
```
**Note:** Different databases use different syntax:
- MySQL: `LIMIT 5`
- SQL Server: `TOP 5`
- PostgreSQL: `LIMIT 5`

---

### 16. SELECT with OFFSET
**Question:** Get the 3rd to 7th highest-paid employees.
```sql
SELECT EmployeeName, Salary FROM Employees 
ORDER BY Salary DESC 
LIMIT 5 OFFSET 2;
```
**Explanation:** OFFSET skips first 2 rows, then LIMIT takes next 5 rows.

---

## Intermediate Queries

### 17. COUNT() Function
**Question:** Count total number of employees.
```sql
SELECT COUNT(*) as TotalEmployees FROM Employees;
```
**Output:**
```
TotalEmployees
---------------
150
```

---

### 18. COUNT with WHERE
**Question:** Count employees in IT department.
```sql
SELECT COUNT(*) as ITEmployees FROM Employees 
WHERE Department = 'IT';
```

---

### 19. SUM() Function
**Question:** Calculate total salary expense.
```sql
SELECT SUM(Salary) as TotalSalaryExpense FROM Employees;
```
**Output:**
```
TotalSalaryExpense
------------------
12500000
```

---

### 20. AVG() Function
**Question:** Calculate average salary.
```sql
SELECT AVG(Salary) as AverageSalary FROM Employees;
```
**Output:**
```
AverageSalary
--------------
65800.50
```

---

### 21. MAX() and MIN() Functions
**Question:** Find highest and lowest salary.
```sql
SELECT 
  MAX(Salary) as HighestSalary,
  MIN(Salary) as LowestSalary 
FROM Employees;
```
**Output:**
```
HighestSalary | LowestSalary
--------------|-------------
150000        | 30000
```

---

### 22. GROUP BY Single Column
**Question:** Get total salary expense by department.
```sql
SELECT Department, SUM(Salary) as DeptSalary 
FROM Employees 
GROUP BY Department;
```
**Explanation:** Combines rows with same Department value and aggregates salary.

**Output:**
```
Department | DeptSalary
-----------|----------
IT         | 850000
HR         | 420000
Finance    | 520000
```

---

### 23. GROUP BY Multiple Columns
**Question:** Get average salary by Department and JobTitle.
```sql
SELECT Department, JobTitle, AVG(Salary) as AvgSalary, COUNT(*) as Count
FROM Employees 
GROUP BY Department, JobTitle;
```
**Explanation:** Groups by both columns, so each combination gets its own group.

---

### 24. HAVING Clause
**Question:** Get departments with more than 10 employees.
```sql
SELECT Department, COUNT(*) as EmployeeCount 
FROM Employees 
GROUP BY Department 
HAVING COUNT(*) > 10;
```
**Explanation:** HAVING filters aggregated results (applies after GROUP BY), whereas WHERE filters before grouping.

---

### 25. GROUP BY with Multiple Aggregates
**Question:** Get statistics by department.
```sql
SELECT 
  Department,
  COUNT(*) as EmployeeCount,
  AVG(Salary) as AvgSalary,
  MAX(Salary) as MaxSalary,
  MIN(Salary) as MinSalary,
  SUM(Salary) as TotalSalary
FROM Employees 
GROUP BY Department;
```

---

### 26. INNER JOIN
**Question:** Get employee names with their department names.
```sql
SELECT e.EmployeeName, d.DepartmentName 
FROM Employees e 
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```
**Explanation:** Returns only rows with matches in both tables.

**Employees Table:**
```
EmployeeID | EmployeeName | DepartmentID
-----------|--------------|-------------
1          | John         | 10
2          | Jane         | 20
3          | Bob          | NULL
```

**Departments Table:**
```
DepartmentID | DepartmentName
-------------|---------------
10           | IT
20           | HR
30           | Finance
```

**Result (INNER JOIN):**
```
EmployeeName | DepartmentName
-------------|---------------
John         | IT
Jane         | HR
```
(Bob excluded because DepartmentID is NULL)

---

### 27. LEFT JOIN
**Question:** Get all employees and their departments (if assigned).
```sql
SELECT e.EmployeeName, d.DepartmentName 
FROM Employees e 
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```
**Explanation:** Returns all rows from LEFT table (Employees) and matching rows from RIGHT table (Departments).

**Result (LEFT JOIN):**
```
EmployeeName | DepartmentName
-------------|---------------
John         | IT
Jane         | HR
Bob          | NULL
```
(All employees included, Bob has NULL department)

---

### 28. RIGHT JOIN
**Question:** Get all departments and their employees (if assigned).
```sql
SELECT e.EmployeeName, d.DepartmentName 
FROM Employees e 
RIGHT JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```
**Explanation:** Returns all rows from RIGHT table (Departments) and matching rows from LEFT table.

**Result (RIGHT JOIN):**
```
EmployeeName | DepartmentName
-------------|---------------
John         | IT
Jane         | HR
NULL         | Finance
```
(All departments included, Finance has no employees)

---

### 29. FULL OUTER JOIN
**Question:** Get all employees and departments.
```sql
SELECT e.EmployeeName, d.DepartmentName 
FROM Employees e 
FULL OUTER JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```
**Explanation:** Returns all rows from both tables.

**Result (FULL OUTER JOIN):**
```
EmployeeName | DepartmentName
-------------|---------------
John         | IT
Jane         | HR
Bob          | NULL
NULL         | Finance
```

---

### 30. CROSS JOIN
**Question:** Get all combinations of employees and projects.
```sql
SELECT e.EmployeeName, p.ProjectName 
FROM Employees e 
CROSS JOIN Projects p;
```
**Explanation:** Creates Cartesian product (each row from first table with each row from second table).

If Employees has 5 rows and Projects has 3 rows, result has 5 Ã— 3 = 15 rows.

---

### 31. Multiple JOINs
**Question:** Get employee name, department, and project information.
```sql
SELECT 
  e.EmployeeName, 
  d.DepartmentName, 
  p.ProjectName,
  p.StartDate
FROM Employees e 
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID 
LEFT JOIN Projects p ON e.EmployeeID = p.AssignedToID;
```

---

### 32. Self JOIN
**Question:** Get each employee's name and their manager's name.
```sql
SELECT 
  e.EmployeeName as Employee,
  m.EmployeeName as Manager
FROM Employees e 
LEFT JOIN Employees m ON e.ManagerID = m.EmployeeID;
```
**Explanation:** Joining a table with itself using aliases.

---

## Advanced Queries

### 33. Subquery in WHERE Clause
**Question:** Get employees earning more than average salary.
```sql
SELECT * FROM Employees 
WHERE Salary > (SELECT AVG(Salary) FROM Employees);
```
**Explanation:** Inner query calculates average, outer query uses it as filter.

---

### 34. Subquery with IN
**Question:** Get employees working on at least one project.
```sql
SELECT * FROM Employees 
WHERE EmployeeID IN (SELECT DISTINCT AssignedToID FROM Projects);
```

---

### 35. Subquery with EXISTS
**Question:** Get departments that have at least one employee.
```sql
SELECT * FROM Departments d 
WHERE EXISTS (
  SELECT 1 FROM Employees e 
  WHERE e.DepartmentID = d.DepartmentID
);
```
**Explanation:** EXISTS returns TRUE if subquery returns any row.

---

### 36. Correlated Subquery
**Question:** Get employees earning more than their department's average.
```sql
SELECT * FROM Employees e1 
WHERE Salary > (
  SELECT AVG(Salary) FROM Employees e2 
  WHERE e2.DepartmentID = e1.DepartmentID
);
```
**Explanation:** Subquery references outer query's columns. Executes once for each outer row.

---

### 37. UNION
**Question:** Combine managers and employees (non-duplicate).
```sql
SELECT EmployeeName FROM Employees 
UNION 
SELECT ManagerName FROM Managers;
```
**Explanation:** Removes duplicate rows. Requires same number and types of columns.

**Result:**
```
Name
----------
John Doe
Jane Smith
(appears only once if in both tables)
```

---

### 38. UNION ALL
**Question:** Combine all managers and employees (including duplicates).
```sql
SELECT EmployeeName FROM Employees 
UNION ALL 
SELECT ManagerName FROM Managers;
```

---

### 39. EXCEPT/MINUS
**Question:** Get employees who are NOT managers.
```sql
SELECT EmployeeID FROM Employees 
EXCEPT 
SELECT ManagerID FROM Managers;
```
**Explanation:** Returns rows from first query that don't exist in second query.

---

### 40. INTERSECT
**Question:** Get employees who are also managers.
```sql
SELECT EmployeeID FROM Employees 
INTERSECT 
SELECT ManagerID FROM Managers;
```
**Explanation:** Returns rows common to both queries.

---

### 41. CASE Statement
**Question:** Categorize employees by salary.
```sql
SELECT 
  EmployeeName,
  Salary,
  CASE 
    WHEN Salary >= 90000 THEN 'Executive'
    WHEN Salary >= 70000 THEN 'Senior'
    WHEN Salary >= 50000 THEN 'Mid-Level'
    ELSE 'Junior'
  END as SalaryLevel
FROM Employees;
```

**Output:**
```
EmployeeName | Salary | SalaryLevel
-------------|--------|----------
Sarah Miller | 95000  | Executive
Jane Smith   | 75000  | Senior
John Doe     | 55000  | Mid-Level
```

---

### 42. CASE with SUM
**Question:** Get salary distribution by level.
```sql
SELECT 
  CASE 
    WHEN Salary >= 90000 THEN 'Executive'
    WHEN Salary >= 70000 THEN 'Senior'
    ELSE 'Junior'
  END as Level,
  COUNT(*) as Count,
  SUM(Salary) as TotalSalary
FROM Employees 
GROUP BY CASE 
  WHEN Salary >= 90000 THEN 'Executive'
  WHEN Salary >= 70000 THEN 'Senior'
  ELSE 'Junior'
END;
```

---

### 43. ROW_NUMBER() Window Function
**Question:** Rank employees by salary within each department.
```sql
SELECT 
  EmployeeName,
  Department,
  Salary,
  ROW_NUMBER() OVER (PARTITION BY Department ORDER BY Salary DESC) as Rank
FROM Employees;
```

**Output:**
```
EmployeeName | Department | Salary | Rank
-------------|------------|--------|-----
Jane Smith   | IT         | 85000  | 1
John Doe     | IT         | 75000  | 2
Sarah Miller | HR         | 95000  | 1
```

---

### 44. RANK() vs DENSE_RANK()
**Question:** Show ranking with and without gaps.
```sql
SELECT 
  EmployeeName,
  Salary,
  RANK() OVER (ORDER BY Salary DESC) as Rank,
  DENSE_RANK() OVER (ORDER BY Salary DESC) as DenseRank
FROM Employees;
```

**Output:**
```
EmployeeName | Salary | Rank | DenseRank
-------------|--------|------|----------
Jane Smith   | 85000  | 1    | 1
Jane Doe     | 85000  | 1    | 1
John Doe     | 75000  | 3    | 2
```

RANK() shows 1, 1, 3 (skips 2). DENSE_RANK() shows 1, 1, 2 (no gaps).

---

### 45. LAG() Function
**Question:** Compare each employee's salary with previous salary.
```sql
SELECT 
  EmployeeName,
  Salary,
  LAG(Salary) OVER (ORDER BY HireDate) as PreviousSalary,
  Salary - LAG(Salary) OVER (ORDER BY HireDate) as Difference
FROM Employees;
```

---

### 46. LEAD() Function
**Question:** Compare current salary with next employee's salary.
```sql
SELECT 
  EmployeeName,
  Salary,
  LEAD(Salary) OVER (ORDER BY Salary DESC) as NextHigherSalary
FROM Employees;
```

---

### 47. Running Total with SUM()
**Question:** Calculate cumulative salary by hire date.
```sql
SELECT 
  EmployeeName,
  HireDate,
  Salary,
  SUM(Salary) OVER (ORDER BY HireDate) as RunningTotal
FROM Employees;
```

---

### 48. NTILE() Function
**Question:** Divide employees into 4 salary quartiles.
```sql
SELECT 
  EmployeeName,
  Salary,
  NTILE(4) OVER (ORDER BY Salary) as Quartile
FROM Employees;
```

---

### 49. INSERT Query
**Question:** Add a new employee.
```sql
INSERT INTO Employees (EmployeeName, Department, Salary, HireDate)
VALUES ('Michael Brown', 'IT', 72000, '2024-01-15');
```

---

### 50. INSERT from SELECT
**Question:** Copy employees from Employees_Archive to Employees.
```sql
INSERT INTO Employees 
SELECT * FROM Employees_Archive 
WHERE HireDate > '2023-01-01';
```

---

### 51. UPDATE Query
**Question:** Give 10% raise to IT department employees.
```sql
UPDATE Employees 
SET Salary = Salary * 1.10 
WHERE Department = 'IT';
```

---

### 52. UPDATE with JOIN
**Question:** Update commission for employees in completed projects.
```sql
UPDATE e 
SET e.Commission = 5000
FROM Employees e 
INNER JOIN Projects p ON e.EmployeeID = p.AssignedToID
WHERE p.Status = 'Completed';
```

---

### 53. DELETE Query
**Question:** Remove employees who haven't been assigned to any project in 2 years.
```sql
DELETE FROM Employees 
WHERE EmployeeID NOT IN (
  SELECT DISTINCT AssignedToID FROM Projects 
  WHERE ProjectDate > DATEADD(YEAR, -2, GETDATE())
);
```

---

### 54. DELETE with JOIN
**Question:** Delete employees from terminated departments.
```sql
DELETE FROM Employees 
WHERE DepartmentID IN (
  SELECT DepartmentID FROM Departments 
  WHERE Status = 'Terminated'
);
```

---

### 55. CTE (Common Table Expression)
**Question:** Get top 3 earners in each department.
```sql
WITH RankedEmployees AS (
  SELECT 
    Department,
    EmployeeName,
    Salary,
    ROW_NUMBER() OVER (PARTITION BY Department ORDER BY Salary DESC) as Rank
  FROM Employees
)
SELECT * FROM RankedEmployees 
WHERE Rank <= 3;
```

---

### 56. Recursive CTE
**Question:** Get employee hierarchy (manager to subordinates).
```sql
WITH EmployeeHierarchy AS (
  -- Base case: all top-level employees
  SELECT EmployeeID, EmployeeName, ManagerID, 0 as Level
  FROM Employees 
  WHERE ManagerID IS NULL
  
  UNION ALL
  
  -- Recursive case: employees under managers
  SELECT e.EmployeeID, e.EmployeeName, e.ManagerID, h.Level + 1
  FROM Employees e 
  INNER JOIN EmployeeHierarchy h ON e.ManagerID = h.EmployeeID
)
SELECT * FROM EmployeeHierarchy 
ORDER BY Level, EmployeeName;
```

---

### 57. String Functions
**Question:** Format employee names and find those with specific pattern.
```sql
SELECT 
  UPPER(EmployeeName) as NameInCaps,
  LOWER(EmployeeName) as NameInLower,
  LENGTH(EmployeeName) as NameLength,
  SUBSTRING(EmployeeName, 1, 3) as FirstThreeLetters
FROM Employees 
WHERE UPPER(EmployeeName) LIKE 'JOHN%';
```

---

### 58. Date Functions
**Question:** Get employees hired in the last 30 days.
```sql
SELECT * FROM Employees 
WHERE HireDate >= DATEADD(DAY, -30, CAST(GETDATE() AS DATE))
AND HireDate <= CAST(GETDATE() AS DATE);
```

---

### 59. Math Functions
**Question:** Round average salary to nearest hundred.
```sql
SELECT 
  Department,
  ROUND(AVG(Salary), -2) as AvgSalaryRounded
FROM Employees 
GROUP BY Department;
```

---

### 60. Conditional Aggregation
**Question:** Get count of employees by status (Active/Inactive).
```sql
SELECT 
  SUM(CASE WHEN Status = 'Active' THEN 1 ELSE 0 END) as ActiveCount,
  SUM(CASE WHEN Status = 'Inactive' THEN 1 ELSE 0 END) as InactiveCount
FROM Employees;
```

---

## Difference Between Questions

### 1. **INNER JOIN vs OUTER JOIN**

| Feature | INNER JOIN | OUTER JOIN |
|---------|-----------|-----------|
| **Definition** | Returns only matching rows from both tables | Returns matching rows + non-matching rows from one/both tables |
| **Null Values** | Does not include NULL | Includes NULL for non-matching rows |
| **Usage** | Strict matching required | Optional matching allowed |
| **Performance** | Faster (filters early) | Slower (processes all rows) |

**Example:**
```sql
-- INNER JOIN
SEL
