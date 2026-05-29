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
# 🗄️ SQL Interview Questions & Answers (Top 40)

> Frequently asked SQL questions covering Basics, Joins, Aggregations, Subqueries, Indexes, Stored Procedures, and more.

---

## 📋 Table of Contents

1. [SQL Basics](#1-sql-basics)
2. [Joins](#2-joins)
3. [Aggregation & Grouping](#3-aggregation--grouping)
4. [Subqueries & CTEs](#4-subqueries--ctes)
5. [Constraints & Keys](#5-constraints--keys)
6. [Indexes & Performance](#6-indexes--performance)
7. [Stored Procedures, Functions & Triggers](#7-stored-procedures-functions--triggers)
8. [Advanced SQL](#8-advanced-sql)
9. [Practical Coding Questions](#9-practical-coding-questions)

---

## 1. SQL Basics

### Q1. What is SQL? What are its sublanguages?

**SQL (Structured Query Language)** is used to communicate with relational databases.

| Sublanguage | Full Form | Commands |
|-------------|-----------|----------|
| **DDL** | Data Definition Language | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML** | Data Manipulation Language | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| **DCL** | Data Control Language | `GRANT`, `REVOKE` |
| **TCL** | Transaction Control Language | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |

---

### Q2. What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?

| Feature | DELETE | TRUNCATE | DROP |
|---------|--------|----------|------|
| Removes | Specific rows | All rows | Entire table |
| WHERE clause | ✅ Yes | ❌ No | ❌ No |
| Rollback | ✅ Possible | ❌ Not possible | ❌ Not possible |
| Triggers fired | ✅ Yes | ❌ No | ❌ No |
| Auto-increment reset | ❌ No | ✅ Yes | — |
| DDL or DML | DML | DDL | DDL |

```sql
DELETE FROM employees WHERE id = 5;   -- deletes one row
TRUNCATE TABLE employees;             -- removes all rows fast
DROP TABLE employees;                 -- removes table entirely
```

---

### Q3. What is the difference between `WHERE` and `HAVING`?

| Feature | WHERE | HAVING |
|---------|-------|--------|
| Used with | Any query | `GROUP BY` |
| Filters | Rows (before grouping) | Groups (after grouping) |
| Aggregate functions | ❌ No | ✅ Yes |

```sql
-- WHERE filters rows before grouping
SELECT department, COUNT(*) 
FROM employees
WHERE salary > 30000
GROUP BY department;

-- HAVING filters groups after aggregation
SELECT department, COUNT(*) AS emp_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

---

### Q4. What is the difference between `UNION` and `UNION ALL`?

| Feature | UNION | UNION ALL |
|---------|-------|-----------|
| Duplicates | Removed | Kept |
| Performance | Slower (removes duplicates) | Faster |
| Use when | Unique results needed | All results including duplicates |

```sql
SELECT city FROM customers
UNION
SELECT city FROM suppliers;      -- unique cities only

SELECT city FROM customers
UNION ALL
SELECT city FROM suppliers;      -- all cities including duplicates
```

---

### Q5. What is a NULL value? How to handle it?

`NULL` means **unknown/missing** — not zero, not empty string.

```sql
-- Check for NULL
SELECT * FROM employees WHERE manager_id IS NULL;
SELECT * FROM employees WHERE manager_id IS NOT NULL;

-- COALESCE: returns first non-null value
SELECT name, COALESCE(phone, email, 'No Contact') AS contact
FROM employees;

-- IFNULL (MySQL) / ISNULL (SQL Server)
SELECT IFNULL(bonus, 0) FROM employees;

-- NULLIF: returns NULL if two values are equal
SELECT NULLIF(score, 0) FROM results; -- returns NULL if score = 0
```

---

### Q6. What are the different types of SQL constraints?

| Constraint | Purpose |
|------------|---------|
| `PRIMARY KEY` | Uniquely identifies each row; NOT NULL + UNIQUE |
| `FOREIGN KEY` | Links to PRIMARY KEY in another table |
| `UNIQUE` | All values in column must be different |
| `NOT NULL` | Column cannot have NULL values |
| `CHECK` | Values must satisfy a condition |
| `DEFAULT` | Assigns a default value when none is provided |

```sql
CREATE TABLE employees (
    id        INT PRIMARY KEY,
    name      VARCHAR(100) NOT NULL,
    email     VARCHAR(100) UNIQUE,
    age       INT CHECK (age >= 18),
    dept_id   INT,
    salary    DECIMAL DEFAULT 30000,
    FOREIGN KEY (dept_id) REFERENCES departments(id)
);
```

---

### Q7. What is normalization? Explain 1NF, 2NF, 3NF.

**Normalization** is the process of organizing database tables to reduce redundancy and improve data integrity.

| Form | Rule |
|------|------|
| **1NF** | Atomic values (no repeating groups or arrays) |
| **2NF** | 1NF + No partial dependency (non-key column depends on full PK) |
| **3NF** | 2NF + No transitive dependency (non-key column depends only on PK) |

---

### Q8. What is a VIEW?

A **virtual table** based on a SELECT query. Does not store data physically.

```sql
-- Create a view
CREATE VIEW high_salary_employees AS
SELECT name, department, salary
FROM employees
WHERE salary > 80000;

-- Use the view
SELECT * FROM high_salary_employees;

-- Drop the view
DROP VIEW high_salary_employees;
```

**Benefits:** Simplifies complex queries, provides security by hiding sensitive columns, reusable.

---

## 2. Joins

### Q9. What are the types of JOINs?

```
INNER JOIN   → Only matching rows in both tables
LEFT JOIN    → All rows from left + matching from right (NULLs where no match)
RIGHT JOIN   → All rows from right + matching from left
FULL JOIN    → All rows from both tables (NULLs where no match)
CROSS JOIN   → Cartesian product (every combination)
SELF JOIN    → Table joined with itself
```

---

### Q10. Explain each JOIN with an example.

**Sample Tables:**
```
employees: id, name, dept_id
departments: id, dept_name
```

```sql
-- INNER JOIN: employees with a matching department
SELECT e.name, d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.id;

-- LEFT JOIN: all employees, even those without a department
SELECT e.name, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id;

-- RIGHT JOIN: all departments, even if no employees
SELECT e.name, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.id;

-- FULL OUTER JOIN: all employees and all departments
SELECT e.name, d.dept_name
FROM employees e
FULL OUTER JOIN departments d ON e.dept_id = d.id;

-- SELF JOIN: find employees and their managers
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

---

### Q11. What is the difference between `ON` and `USING` in a JOIN?

```sql
-- ON: flexible, used when column names differ
SELECT * FROM employees e
JOIN departments d ON e.dept_id = d.id;

-- USING: shorthand when column name is same in both tables
SELECT * FROM employees
JOIN departments USING (dept_id);
```

---

## 3. Aggregation & Grouping

### Q12. What are aggregate functions?

| Function | Description |
|----------|-------------|
| `COUNT()` | Number of rows |
| `SUM()` | Total of values |
| `AVG()` | Average value |
| `MIN()` | Minimum value |
| `MAX()` | Maximum value |

```sql
SELECT
    COUNT(*) AS total_employees,
    AVG(salary) AS avg_salary,
    MAX(salary) AS highest_salary,
    MIN(salary) AS lowest_salary,
    SUM(salary) AS total_payroll
FROM employees;
```

---

### Q13. What does `GROUP BY` do?

Groups rows with the same value in specified columns so aggregate functions can be applied per group.

```sql
-- Salary stats per department
SELECT department, COUNT(*) AS headcount, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY avg_salary DESC;
```

**Rule:** Every column in SELECT (that's not an aggregate) **must** appear in GROUP BY.

---

### Q14. What are Window Functions?

Perform calculations **across a set of rows related to the current row**, without collapsing them.

```sql
-- ROW_NUMBER: unique rank per partition
SELECT name, department, salary,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rn
FROM employees;

-- RANK vs DENSE_RANK
-- RANK: 1,1,3 (skips 2)   DENSE_RANK: 1,1,2 (no skip)
SELECT name, salary,
    RANK() OVER (ORDER BY salary DESC) AS rnk,
    DENSE_RANK() OVER (ORDER BY salary DESC) AS dense_rnk
FROM employees;

-- LAG / LEAD: access previous/next row value
SELECT name, salary,
    LAG(salary) OVER (ORDER BY id) AS prev_salary,
    LEAD(salary) OVER (ORDER BY id) AS next_salary
FROM employees;

-- Running total
SELECT name, salary,
    SUM(salary) OVER (ORDER BY id) AS running_total
FROM employees;
```

---

## 4. Subqueries & CTEs

### Q15. What is a subquery?

A query **nested inside** another query.

```sql
-- Scalar subquery (returns one value)
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);

-- IN subquery (returns a list)
SELECT name FROM employees
WHERE dept_id IN (SELECT id FROM departments WHERE location = 'New York');

-- EXISTS subquery (checks existence)
SELECT name FROM employees e
WHERE EXISTS (
    SELECT 1 FROM orders o WHERE o.emp_id = e.id
);

-- Correlated subquery (references outer query)
SELECT name, salary FROM employees e1
WHERE salary = (
    SELECT MAX(salary) FROM employees e2
    WHERE e1.dept_id = e2.dept_id
);
```

---

### Q16. What is a CTE (Common Table Expression)?

A **named temporary result set** defined using `WITH`, valid for a single query.

```sql
-- Simple CTE
WITH dept_avg AS (
    SELECT dept_id, AVG(salary) AS avg_sal
    FROM employees
    GROUP BY dept_id
)
SELECT e.name, e.salary, da.avg_sal
FROM employees e
JOIN dept_avg da ON e.dept_id = da.dept_id
WHERE e.salary > da.avg_sal;

-- Recursive CTE: employee hierarchy
WITH RECURSIVE emp_hierarchy AS (
    SELECT id, name, manager_id, 1 AS level
    FROM employees WHERE manager_id IS NULL  -- root (CEO)
    UNION ALL
    SELECT e.id, e.name, e.manager_id, eh.level + 1
    FROM employees e
    JOIN emp_hierarchy eh ON e.manager_id = eh.id
)
SELECT * FROM emp_hierarchy ORDER BY level;
```

---

### Q17. What is the difference between a subquery and a CTE?

| Feature | Subquery | CTE |
|---------|----------|-----|
| Readability | Can be complex | More readable |
| Reuse in same query | ❌ No | ✅ Yes (reference multiple times) |
| Recursion | ❌ No | ✅ Yes |
| Performance | Similar | Similar (optimizer treats equally) |

---

## 5. Constraints & Keys

### Q18. What is the difference between Primary Key and Unique Key?

| Feature | Primary Key | Unique Key |
|---------|-------------|------------|
| NULL allowed | ❌ No | ✅ One NULL allowed |
| Per table | Only one | Multiple allowed |
| Index created | Clustered | Non-clustered |
| Purpose | Row identity | Enforce uniqueness |

---

### Q19. What is a Foreign Key? What is referential integrity?

A **Foreign Key** is a column that references the Primary Key of another table.

**Referential integrity** ensures a FK value must exist in the referenced table or be NULL.

```sql
CREATE TABLE orders (
    order_id   INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
        ON DELETE CASCADE      -- delete orders when customer deleted
        ON UPDATE CASCADE      -- update FK when PK updated
);
```

**ON DELETE options:** `CASCADE`, `SET NULL`, `RESTRICT`, `NO ACTION`

---

### Q20. What is a composite key?

A **primary key made of two or more columns** together.

```sql
CREATE TABLE order_items (
    order_id   INT,
    product_id INT,
    quantity   INT,
    PRIMARY KEY (order_id, product_id)  -- composite key
);
```

---

## 6. Indexes & Performance

### Q21. What is an Index? Why use it?

An index is a **data structure** (B-Tree by default) that speeds up data retrieval.

```sql
-- Create index
CREATE INDEX idx_emp_name ON employees(name);

-- Create unique index
CREATE UNIQUE INDEX idx_emp_email ON employees(email);

-- Composite index
CREATE INDEX idx_dept_sal ON employees(department, salary);

-- Drop index
DROP INDEX idx_emp_name ON employees;
```

**Trade-offs:**
- ✅ Faster SELECT queries
- ❌ Slower INSERT/UPDATE/DELETE (index must update too)
- ❌ Extra storage space

---

### Q22. What is the difference between Clustered and Non-Clustered Index?

| Feature | Clustered | Non-Clustered |
|---------|-----------|---------------|
| Data storage | Sorted physically by index | Separate index structure |
| Per table | Only **one** | Multiple allowed |
| Speed | Faster for range queries | Faster for exact lookups |
| Auto-created for | PRIMARY KEY | UNIQUE constraint |

---

### Q23. What is query optimization? What is EXPLAIN?

`EXPLAIN` shows how the query engine executes a query — helps identify slow operations.

```sql
EXPLAIN SELECT * FROM employees WHERE department = 'Engineering';
-- Look for: type=ALL (full scan = slow), type=ref (index used = fast)
```

**Common optimizations:**
- Add indexes on WHERE, JOIN, ORDER BY columns
- Avoid `SELECT *` — select only needed columns
- Avoid functions on indexed columns in WHERE: `WHERE YEAR(created_at) = 2024` (bad) → `WHERE created_at BETWEEN '2024-01-01' AND '2024-12-31'` (good)
- Use `LIMIT` for large result sets
- Avoid `DISTINCT` unless necessary

---

## 7. Stored Procedures, Functions & Triggers

### Q24. What is a Stored Procedure?

A **precompiled SQL block** stored in the database, executed by calling its name.

```sql
-- Create stored procedure
DELIMITER //
CREATE PROCEDURE GetEmployeesByDept(IN dept_name VARCHAR(50))
BEGIN
    SELECT name, salary
    FROM employees
    WHERE department = dept_name
    ORDER BY salary DESC;
END //
DELIMITER ;

-- Call it
CALL GetEmployeesByDept('Engineering');
```

**Benefits:** Reusability, security (no raw SQL exposure), performance (precompiled).

---

### Q25. What is the difference between Stored Procedure and Function?

| Feature | Stored Procedure | Function |
|---------|-----------------|----------|
| Returns value | Optional (OUT params) | Must return a value |
| Called with | `CALL` | Used in SQL expressions |
| DML inside | ✅ Yes | Limited (depends on DB) |
| Transactions | ✅ Yes | Limited |
| Use case | Business logic | Calculations, transformations |

```sql
-- Function example
CREATE FUNCTION GetFullName(first VARCHAR(50), last VARCHAR(50))
RETURNS VARCHAR(100)
DETERMINISTIC
BEGIN
    RETURN CONCAT(first, ' ', last);
END;

-- Use in query
SELECT GetFullName(first_name, last_name) AS full_name FROM employees;
```

---

### Q26. What is a Trigger?

A **block of SQL that automatically executes** in response to INSERT, UPDATE, or DELETE.

```sql
CREATE TRIGGER before_employee_insert
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF NEW.salary < 0 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Salary cannot be negative';
    END IF;
END;

-- Audit trigger: log changes
CREATE TRIGGER after_salary_update
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
    INSERT INTO salary_audit(emp_id, old_salary, new_salary, changed_at)
    VALUES (OLD.id, OLD.salary, NEW.salary, NOW());
END;
```

---

## 8. Advanced SQL

### Q27. What are Transactions? What are ACID properties?

A **transaction** is a sequence of SQL operations treated as one unit.

| Property | Meaning |
|----------|---------|
| **A**tomicity | All or nothing — if one step fails, whole transaction rolls back |
| **C**onsistency | Database moves from one valid state to another |
| **I**solation | Concurrent transactions don't interfere with each other |
| **D**urability | Committed changes survive crashes |

```sql
BEGIN TRANSACTION;
    UPDATE accounts SET balance = balance - 1000 WHERE id = 1;
    UPDATE accounts SET balance = balance + 1000 WHERE id = 2;
COMMIT;

-- If something goes wrong
ROLLBACK;

-- Partial rollback
SAVEPOINT sp1;
UPDATE ...;
ROLLBACK TO sp1;
```

---

### Q28. What are Transaction Isolation Levels?

| Level | Dirty Read | Non-Repeatable Read | Phantom Read |
|-------|:----------:|:-------------------:|:------------:|
| READ UNCOMMITTED | ✅ Possible | ✅ Possible | ✅ Possible |
| READ COMMITTED | ❌ | ✅ Possible | ✅ Possible |
| REPEATABLE READ | ❌ | ❌ | ✅ Possible |
| SERIALIZABLE | ❌ | ❌ | ❌ |

- **Higher isolation = more consistency but less concurrency**
- Default in MySQL: `REPEATABLE READ`
- Default in PostgreSQL: `READ COMMITTED`

---

### Q29. What is the difference between OLTP and OLAP?

| Feature | OLTP | OLAP |
|---------|------|------|
| Purpose | Day-to-day transactions | Analytics & reporting |
| Operations | INSERT, UPDATE, DELETE | SELECT (complex queries) |
| Data size | Small per transaction | Large datasets |
| Speed | Fast (milliseconds) | Slower (seconds/minutes) |
| Normalization | Highly normalized | De-normalized (star schema) |
| Example | Banking system | Data Warehouse |

---

### Q30. What is `CASE` expression?

Like an if-else inside SQL.

```sql
-- Simple CASE
SELECT name, salary,
    CASE
        WHEN salary >= 100000 THEN 'High'
        WHEN salary >= 50000  THEN 'Medium'
        ELSE 'Low'
    END AS salary_band
FROM employees;

-- CASE in aggregation
SELECT
    SUM(CASE WHEN department = 'Engineering' THEN salary ELSE 0 END) AS eng_payroll,
    SUM(CASE WHEN department = 'Sales' THEN salary ELSE 0 END) AS sales_payroll
FROM employees;
```

---

### Q31. What is `PIVOT`?

Transforms rows into columns (rotating data).

```sql
-- MySQL approach using CASE
SELECT
    year,
    SUM(CASE WHEN quarter = 'Q1' THEN revenue END) AS Q1,
    SUM(CASE WHEN quarter = 'Q2' THEN revenue END) AS Q2,
    SUM(CASE WHEN quarter = 'Q3' THEN revenue END) AS Q3,
    SUM(CASE WHEN quarter = 'Q4' THEN revenue END) AS Q4
FROM sales
GROUP BY year;
```

---

### Q32. What is the difference between `CHAR` and `VARCHAR`?

| Feature | CHAR | VARCHAR |
|---------|------|---------|
| Length | Fixed | Variable |
| Storage | Pads with spaces | Only uses actual length |
| Speed | Slightly faster | Slightly slower |
| Use when | Fixed-length data (codes, flags) | Variable-length data (names) |

```sql
CHAR(10)     -- always uses 10 bytes
VARCHAR(10)  -- uses only as many bytes as needed (+ 1-2 overhead)
```

---

## 9. Practical Coding Questions

### Q33. Find the second highest salary

```sql
-- Using LIMIT/OFFSET
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 1;

-- Using subquery (works everywhere)
SELECT MAX(salary) AS second_highest
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);

-- Using DENSE_RANK (returns NULL if doesn't exist)
SELECT salary FROM (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM employees
) ranked
WHERE rnk = 2;
```

---

### Q34. Find duplicate records

```sql
-- Find emails that appear more than once
SELECT email, COUNT(*) AS occurrences
FROM employees
GROUP BY email
HAVING COUNT(*) > 1;

-- Show all duplicate rows
SELECT * FROM employees
WHERE email IN (
    SELECT email FROM employees
    GROUP BY email HAVING COUNT(*) > 1
);
```

---

### Q35. Delete duplicate rows keeping one

```sql
-- Keep the row with the lowest id
DELETE FROM employees
WHERE id NOT IN (
    SELECT MIN(id) FROM employees GROUP BY email
);

-- Using ROW_NUMBER (SQL Server / PostgreSQL)
WITH ranked AS (
    SELECT id, ROW_NUMBER() OVER (PARTITION BY email ORDER BY id) AS rn
    FROM employees
)
DELETE FROM employees WHERE id IN (SELECT id FROM ranked WHERE rn > 1);
```

---

### Q36. Find employees with salary greater than their department average

```sql
SELECT e.name, e.department, e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(salary) FROM employees
    WHERE department = e.department
);

-- Using window function (more efficient)
SELECT name, department, salary FROM (
    SELECT name, department, salary,
        AVG(salary) OVER (PARTITION BY department) AS dept_avg
    FROM employees
) t
WHERE salary > dept_avg;
```

---

### Q37. Find the Nth highest salary

```sql
-- Find Nth highest (e.g., 3rd)
SELECT DISTINCT salary FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET N-1;  -- replace N with actual number e.g. OFFSET 2 for 3rd

-- Dynamic using variable (MySQL)
SET @N = 3;
SELECT salary FROM (
    SELECT DISTINCT salary,
        DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM employees
) ranked
WHERE rnk = @N;
```

---

### Q38. G
# 🏋️ SQL Practice Questions (35 Problems with Solutions)

> Hands-on SQL practice problems from Basic to Advanced level. Try solving yourself first, then check the solution!

---

## 📦 Sample Database Schema

> All questions below use these tables. Set them up first!

```sql
-- DEPARTMENTS table
CREATE TABLE departments (
    dept_id   INT PRIMARY KEY,
    dept_name VARCHAR(50),
    location  VARCHAR(50)
);

-- EMPLOYEES table
CREATE TABLE employees (
    emp_id     INT PRIMARY KEY,
    name       VARCHAR(100),
    dept_id    INT,
    salary     DECIMAL(10,2),
    manager_id INT,
    join_date  DATE,
    gender     VARCHAR(10),
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);

-- PRODUCTS table
CREATE TABLE products (
    product_id   INT PRIMARY KEY,
    product_name VARCHAR(100),
    category     VARCHAR(50),
    price        DECIMAL(10,2),
    stock        INT
);

-- ORDERS table
CREATE TABLE orders (
    order_id   INT PRIMARY KEY,
    emp_id     INT,
    product_id INT,
    quantity   INT,
    order_date DATE,
    status     VARCHAR(20),
    FOREIGN KEY (emp_id)     REFERENCES employees(emp_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);

-- SALES table
CREATE TABLE sales (
    sale_id     INT PRIMARY KEY,
    emp_id      INT,
    sale_amount DECIMAL(10,2),
    sale_date   DATE,
    region      VARCHAR(50)
);
```

---

```sql
-- Sample Data

INSERT INTO departments VALUES
(1, 'Engineering',  'New York'),
(2, 'Sales',        'Chicago'),
(3, 'HR',           'New York'),
(4, 'Marketing',    'Los Angeles'),
(5, 'Finance',      'Chicago');

INSERT INTO employees VALUES
(1,  'Alice',   1, 95000, NULL, '2019-03-15', 'Female'),
(2,  'Bob',     1, 85000, 1,    '2020-06-01', 'Male'),
(3,  'Charlie', 2, 60000, NULL, '2018-11-20', 'Male'),
(4,  'Diana',   2, 72000, 3,    '2021-01-10', 'Female'),
(5,  'Ethan',   3, 55000, 1,    '2022-07-05', 'Male'),
(6,  'Fiona',   3, 58000, 1,    '2020-09-18', 'Female'),
(7,  'George',  4, 67000, NULL, '2017-04-22', 'Male'),
(8,  'Helen',   4, 71000, 7,    '2023-02-14', 'Female'),
(9,  'Ivan',    5, 90000, 1,    '2019-08-30', 'Male'),
(10, 'Julia',   5, 88000, 9,    '2021-05-11', 'Female'),
(11, 'Kevin',   1, 95000, 1,    '2020-03-25', 'Male'),
(12, 'Laura',   2, 60000, 3,    '2022-12-01', 'Female');

INSERT INTO products VALUES
(1, 'Laptop',   'Electronics', 1200.00, 50),
(2, 'Phone',    'Electronics',  800.00, 100),
(3, 'Desk',     'Furniture',    300.00, 30),
(4, 'Chair',    'Furniture',    150.00, 80),
(5, 'Monitor',  'Electronics',  400.00, 60),
(6, 'Keyboard', 'Electronics',   80.00, 200),
(7, 'Notebook', 'Stationery',    10.00, 500),
(8, 'Pen',      'Stationery',     2.00, 1000);

INSERT INTO orders VALUES
(1,  3, 1, 2, '2024-01-10', 'Completed'),
(2,  5, 2, 1, '2024-01-15', 'Completed'),
(3,  1, 3, 5, '2024-02-01', 'Pending'),
(4,  7, 4, 3, '2024-02-10', 'Completed'),
(5,  2, 5, 1, '2024-02-20', 'Cancelled'),
(6,  4, 6, 4, '2024-03-05', 'Completed'),
(7,  6, 1, 1, '2024-03-12', 'Completed'),
(8,  9, 2, 2, '2024-03-18', 'Pending'),
(9,  3, 7, 10,'2024-04-02', 'Completed'),
(10, 1, 8, 20,'2024-04-15', 'Completed');

INSERT INTO sales VALUES
(1,  3,  15000, '2024-01-05', 'North'),
(2,  4,  22000, '2024-01-20', 'South'),
(3,  3,  18000, '2024-02-10', 'North'),
(4,  4,  30000, '2024-02-28', 'East'),
(5,  12, 12000, '2024-03-05', 'North'),
(6,  3,  25000, '2024-03-15', 'West'),
(7,  4,  19000, '2024-04-01', 'South'),
(8,  12, 27000, '2024-04-10', 'East'),
(9,  3,  31000, '2024-05-02', 'West'),
(10, 4,  16000, '2024-05-20', 'North');
```

---

## 🟢 EASY (Q1 – Q12)

---

### Q1. List all employees with their department name.

<details>
<summary>💡 Hint</summary>
Use JOIN between employees and departments.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT e.emp_id, e.name, d.dept_name, e.salary
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
ORDER BY d.dept_name;
```
</details>

---

### Q2. Find all employees whose salary is greater than 80,000.

<details>
<summary>✅ Solution</summary>

```sql
SELECT name, salary, dept_id
FROM employees
WHERE salary > 80000
ORDER BY salary DESC;
```
</details>

---

### Q3. Count the number of employees in each department.

<details>
<summary>✅ Solution</summary>

```sql
SELECT d.dept_name, COUNT(e.emp_id) AS total_employees
FROM departments d
LEFT JOIN employees e ON d.dept_id = e.dept_id
GROUP BY d.dept_name
ORDER BY total_employees DESC;
```
</details>

---

### Q4. Find the highest and lowest salary in the company.

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    MAX(salary) AS highest_salary,
    MIN(salary) AS lowest_salary,
    AVG(salary) AS avg_salary
FROM employees;
```
</details>

---

### Q5. List all products in the 'Electronics' category with price less than 500.

<details>
<summary>✅ Solution</summary>

```sql
SELECT product_name, price, stock
FROM products
WHERE category = 'Electronics' AND price < 500
ORDER BY price;
```
</details>

---

### Q6. Find employees who do NOT have a manager (top-level managers).

<details>
<summary>💡 Hint</summary>
Check for NULL in manager_id.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT emp_id, name, dept_id, salary
FROM employees
WHERE manager_id IS NULL;
```
</details>

---

### Q7. List all orders that are 'Completed', sorted by order_date descending.

<details>
<summary>✅ Solution</summary>

```sql
SELECT o.order_id, e.name AS employee, p.product_name, o.quantity, o.order_date
FROM orders o
JOIN employees e ON o.emp_id = e.emp_id
JOIN products p ON o.product_id = p.product_id
WHERE o.status = 'Completed'
ORDER BY o.order_date DESC;
```
</details>

---

### Q8. Find the total number of orders per status.

<details>
<summary>✅ Solution</summary>

```sql
SELECT status, COUNT(*) AS total_orders
FROM orders
GROUP BY status
ORDER BY total_orders DESC;
```
</details>

---

### Q9. Get all employees who joined after January 1, 2021.

<details>
<summary>✅ Solution</summary>

```sql
SELECT name, join_date, dept_id
FROM employees
WHERE join_date > '2021-01-01'
ORDER BY join_date;
```
</details>

---

### Q10. Find the average salary per department.

<details>
<summary>✅ Solution</summary>

```sql
SELECT d.dept_name, ROUND(AVG(e.salary), 2) AS avg_salary
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
GROUP BY d.dept_name
ORDER BY avg_salary DESC;
```
</details>

---

### Q11. Find all employees whose name starts with 'A' or ends with 'a'.

<details>
<summary>💡 Hint</summary>
Use LIKE operator.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT name, salary
FROM employees
WHERE name LIKE 'A%' OR name LIKE '%a'
ORDER BY name;
```
</details>

---

### Q12. Calculate the total order value (quantity × price) for each order.

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    o.order_id,
    e.name AS employee,
    p.product_name,
    o.quantity,
    p.price,
    (o.quantity * p.price) AS total_value
FROM orders o
JOIN employees e ON o.emp_id = e.emp_id
JOIN products p ON o.product_id = p.product_id
ORDER BY total_value DESC;
```
</details>

---

## 🟡 MEDIUM (Q13 – Q26)

---

### Q13. Find departments where average salary is greater than 70,000.

<details>
<summary>💡 Hint</summary>
Use GROUP BY + HAVING.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT d.dept_name, ROUND(AVG(e.salary), 2) AS avg_salary
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
GROUP BY d.dept_name
HAVING AVG(e.salary) > 70000
ORDER BY avg_salary DESC;
```
</details>

---

### Q14. Find the second highest salary in the company.

<details>
<summary>✅ Solution</summary>

```sql
-- Method 1: Subquery
SELECT MAX(salary) AS second_highest
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);

-- Method 2: DENSE_RANK
SELECT salary FROM (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM employees
) t
WHERE rnk = 2;
```
</details>

---

### Q15. List employees along with their manager's name.

<details>
<summary>💡 Hint</summary>
Use SELF JOIN on employees table.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    e.name   AS employee,
    e.salary AS emp_salary,
    COALESCE(m.name, 'No Manager') AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.emp_id
ORDER BY manager;
```
</details>

---

### Q16. Find all employees who earn more than the average salary of their department.

<details>
<summary>✅ Solution</summary>

```sql
-- Using correlated subquery
SELECT e.name, e.salary, d.dept_name
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
WHERE e.salary > (
    SELECT AVG(salary) FROM employees
    WHERE dept_id = e.dept_id
);

-- Using window function (cleaner)
SELECT name, dept_name, salary FROM (
    SELECT e.name, d.dept_name, e.salary,
        AVG(e.salary) OVER (PARTITION BY e.dept_id) AS dept_avg
    FROM employees e
    JOIN departments d ON e.dept_id = d.dept_id
) t
WHERE salary > dept_avg;
```
</details>

---

### Q17. Find duplicate salary values in the employees table.

<details>
<summary>✅ Solution</summary>

```sql
SELECT salary, COUNT(*) AS occurrences
FROM employees
GROUP BY salary
HAVING COUNT(*) > 1
ORDER BY salary DESC;
```
</details>

---

### Q18. Find employees who have NOT placed any orders.

<details>
<summary>💡 Hint</summary>
Use LEFT JOIN + IS NULL, or NOT IN / NOT EXISTS.
</details>

<details>
<summary>✅ Solution</summary>

```sql
-- Method 1: LEFT JOIN
SELECT e.emp_id, e.name, e.dept_id
FROM employees e
LEFT JOIN orders o ON e.emp_id = o.emp_id
WHERE o.order_id IS NULL;

-- Method 2: NOT EXISTS
SELECT emp_id, name FROM employees e
WHERE NOT EXISTS (
    SELECT 1 FROM orders o WHERE o.emp_id = e.emp_id
);
```
</details>

---

### Q19. Rank employees by salary within each department.

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    e.name,
    d.dept_name,
    e.salary,
    RANK()       OVER (PARTITION BY e.dept_id ORDER BY e.salary DESC) AS rank_in_dept,
    DENSE_RANK() OVER (PARTITION BY e.dept_id ORDER BY e.salary DESC) AS dense_rank_in_dept
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
ORDER BY d.dept_name, rank_in_dept;
```
</details>

---

### Q20. Get the top 1 highest-paid employee in each department.

<details>
<summary>✅ Solution</summary>

```sql
SELECT name, dept_name, salary FROM (
    SELECT e.name, d.dept_name, e.salary,
        ROW_NUMBER() OVER (PARTITION BY e.dept_id ORDER BY e.salary DESC) AS rn
    FROM employees e
    JOIN departments d ON e.dept_id = d.dept_id
) t
WHERE rn = 1;
```
</details>

---

### Q21. Calculate the running total of sales by date.

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    sale_date,
    emp_id,
    sale_amount,
    SUM(sale_amount) OVER (ORDER BY sale_date) AS running_total,
    SUM(sale_amount) OVER (
        PARTITION BY emp_id ORDER BY sale_date
    ) AS running_total_per_emp
FROM sales
ORDER BY sale_date;
```
</details>

---

### Q22. Find the month-wise total sales amount.

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    YEAR(sale_date)  AS year,
    MONTH(sale_date) AS month,
    SUM(sale_amount) AS total_sales,
    COUNT(*)         AS num_transactions
FROM sales
GROUP BY YEAR(sale_date), MONTH(sale_date)
ORDER BY year, month;
```
</details>

---

### Q23. Find products that have never been ordered.

<details>
<summary>✅ Solution</summary>

```sql
SELECT p.product_id, p.product_name, p.category
FROM products p
LEFT JOIN orders o ON p.product_id = o.product_id
WHERE o.order_id IS NULL;
```
</details>

---

### Q24. Get each employee's salary compared to the previous employee (by join date).

<details>
<summary>💡 Hint</summary>
Use LAG window function.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    name,
    join_date,
    salary,
    LAG(salary) OVER (ORDER BY join_date) AS prev_emp_salary,
    salary - LAG(salary) OVER (ORDER BY join_date) AS salary_diff
FROM employees
ORDER BY join_date;
```
</details>

---

### Q25. Find employees whose salary is in the top 25% of the company.

<details>
<summary>✅ Solution</summary>

```sql
SELECT name, salary FROM (
    SELECT name, salary,
        NTILE(4) OVER (ORDER BY salary DESC) AS quartile
    FROM employees
) t
WHERE quartile = 1
ORDER BY salary DESC;
```
</details>

---

### Q26. Find the cumulative percentage of total sales per employee.

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    emp_id,
    SUM(sale_amount) AS total_sales,
    ROUND(
        100.0 * SUM(sale_amount) / SUM(SUM(sale_amount)) OVER (),
        2
    ) AS pct_of_total
FROM sales
GROUP BY emp_id
ORDER BY total_sales DESC;
```
</details>

---

## 🔴 HARD (Q27 – Q35)

---

### Q27. Write a query to get the Nth highest salary (e.g., 3rd highest).

<details>
<summary>✅ Solution</summary>

```sql
-- Set N = 3 (change as needed)
SELECT DISTINCT salary FROM (
    SELECT salary,
        DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM employees
) t
WHERE rnk = 3;

-- General form using variable (MySQL)
SET @N = 3;
SELECT salary FROM (
    SELECT DISTINCT salary,
        DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM employees
) t
WHERE rnk = @N;
```
</details>

---

### Q28. Find employees who joined in the same month and year as another employee.

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    e1.name AS employee,
    e2.name AS joined_same_month_as,
    e1.join_date
FROM employees e1
JOIN employees e2
    ON  YEAR(e1.join_date)  = YEAR(e2.join_date)
    AND MONTH(e1.join_date) = MONTH(e2.join_date)
    AND e1.emp_id < e2.emp_id
ORDER BY e1.join_date;
```
</details>

---

### Q29. Get the department with the highest total salary bill.

<details>
<summary>✅ Solution</summary>

```sql
-- Single department (top 1)
SELECT d.dept_name, SUM(e.salary) AS total_salary_bill
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
GROUP BY d.dept_name
ORDER BY total_salary_bill DESC
LIMIT 1;

-- Using CTE with RANK
WITH dept_totals AS (
    SELECT d.dept_name, SUM(e.salary) AS total_salary_bill,
        RANK() OVER (ORDER BY SUM(e.salary) DESC) AS rnk
    FROM employees e
    JOIN departments d ON e.dept_id = d.dept_id
    GROUP BY d.dept_name
)
SELECT dept_name, total_salary_bill FROM dept_totals WHERE rnk = 1;
```
</details>

---

### Q30. Find employees whose salary is above average AND who have placed at least one order.

<details>
<summary>✅ Solution</summary>

```sql
SELECT DISTINCT e.name, e.salary
FROM employees e
JOIN orders o ON e.emp_id = o.emp_id
WHERE e.salary > (SELECT AVG(salary) FROM employees)
ORDER BY e.salary DESC;
```
</details>

---

### Q31. Create a report: for each department show total employees, avg salary, min salary, max salary.

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    d.dept_name,
    d.location,
    COUNT(e.emp_id)       AS total_employees,
    ROUND(AVG(e.salary), 2) AS avg_salary,
    MIN(e.salary)         AS min_salary,
    MAX(e.salary)         AS max_salary,
    SUM(e.salary)         AS total_payroll
FROM departments d
LEFT JOIN employees e ON d.dept_id = e.dept_id
GROUP BY d.dept_name, d.location
ORDER BY total_payroll DESC;
```
</details>

---

### Q32. Find the employee with the most orders placed.

<details>
<summary>✅ Solution</summary>

```sql
-- Using subquery
SELECT e.name, COUNT(o.order_id) AS order_count
FROM employees e
JOIN orders o ON e.emp_id = o.emp_id
GROUP BY e.emp_id, e.name
ORDER BY order_count DESC
LIMIT 1;

-- Using CTE (handles ties)
WITH order_counts AS (
    SELECT emp_id, COUNT(*) AS order_count,
        RANK() OVER (ORDER BY COUNT(*) DESC) AS rnk
    FROM orders
    GROUP BY emp_id
)
SELECT e.name, oc.order_count
FROM order_counts oc
JOIN employees e ON oc.emp_id = e.emp_id
WHERE rnk = 1;
```
</details>

---

### Q33. Pivot: Show total sales amount per employee per region (rows = employees, columns = regions).

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    e.name,
    SUM(CASE WHEN s.region = 'North' THEN s.sale_amount ELSE 0 END) AS North,
    SUM(CASE WHEN s.region = 'South' THEN s.sale_amount ELSE 0 END) AS South,
    SUM(CASE WHEN s.region = 'East'  THEN s.sale_amount ELSE 0 END) AS East,
    SUM(CASE WHEN s.region = 'West'  THEN s.sale_amount ELSE 0 END) AS West,
    SUM(s.sale_amount) AS Total
FROM sales s
JOIN employees e ON s.emp_id = e.emp_id
GROUP BY e.emp_id, e.name
ORDER BY Total DESC;
```
</details>

---

### Q34. For each employee in Sales dept, show their sales growth month over month.

<details>
<summary>✅ Solution</summary>

```sql
WITH monthly_sales AS (
    SELECT
        emp_id,
        DATE_FORMAT(sale_date, '%Y-%m') AS yr_month,
        SUM(sale_amount) AS monthly_total
    FROM sales
    GROUP BY emp_id, DATE_FORMAT(sale_date, '%Y-%m')
),
sales_with_prev AS (
    SELECT
        emp_id,
        yr_month,
        monthly_total,
        LAG(monthly_total) OVER (PARTITION BY emp_id ORDER BY yr_month) AS prev_month
    FROM monthly_sales
)
SELECT
    e.name,
    s.yr_month,
    s.monthly_total,
    s.prev_month,
    ROUND(
        CASE
            WHEN prev_month IS NULL OR prev_month = 0 THEN NULL
            ELSE 100.0 * (monthly_total - prev_month) / prev_month
        END, 2
    ) AS growth_pct
FROM sales_with_prev s
JOIN employees e ON s.emp_id = e.emp_id
ORDER BY e.name, s.yr_month;
```
</details>

---

### Q35. Find all pairs of employees in the same department who have the same salary.

<details>
<summary>✅ Solution</summary>

```sql
SELECT
    e1.name  AS employee_1,
    e2.name  AS employee_2,
    d.dept_name,
    e1.salary
FROM employees e1
JOIN employees e2
    ON  e1.dept_id = e2.dept_id
    AND e1.salary  = e2.salary
    AND e1.emp_id  < e2.emp_id   -- avoid duplicates & self pairs
JOIN departments d ON e1.dept_id = d.dept_id
ORDER BY e1.salary DESC;
```
</details>

---

## 📊 Difficulty Summary

| Level | Questions | Topics Covered |
|-------|-----------|----------------|
| 🟢 Easy | Q1 – Q12 | SELECT, WHERE, JOIN, GROUP BY, ORDER BY, LIKE, NULL |
| 🟡 Medium | Q13 – Q26 | HAVING, Subqueries, SELF JOIN, Window Functions, LAG/LEAD |
| 🔴 Hard | Q27 – Q35 | CTEs, PIVOT, Recursive patterns, Complex aggregations |

---

## 💡 Key Concepts Used

| Concept | Questions |
|---------|-----------|
| INNER / LEFT JOIN | Q1, Q7, Q15, Q18, Q23 |
| GROUP BY + HAVING | Q3, Q10, Q13, Q17 |
| Subqueries | Q14, Q16, Q18, Q30 |
| SELF JOIN | Q15, Q28, Q35 |
| Window Functions | Q19, Q20, Q21, Q24, Q25, Q27 |
| CTE (WITH clause) | Q16, Q29, Q32, Q34 |
| LAG / LEAD | Q24, Q34 |
| CASE / PIVOT | Q33 |
| NOT IN / NOT EXISTS | Q18, Q23 |
| Date Functions | Q9, Q22, Q28, Q34 |

---

## 🧠 Practice Tips

1. **Always read the question twice** before writing SQL
2. **Sketch the expected output** — know what rows/columns you want
3. **Build the query step by step** — start with FROM + JOIN, then WHERE, then GROUP BY
4. **Test with LIMIT 5** first to preview data before running full query
5. **Window functions** are the most tested in senior interviews — master them!
6. **CTEs > Nested subqueries** for readability — practice rewriting subqueries as CTEs
7. **Execution order to remember:**
   ```
   FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT
   ```

---

*Happy Practicing! 🚀 Keep solving daily and you'll crack any SQL interview.*
