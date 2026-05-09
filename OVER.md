# OVER Clause in PostgreSQL

## What is OVER Clause?

The `OVER()` clause is used with **window functions**.

It performs calculations across a set of rows related to the current row **without grouping rows into a single result**.

Difference:

- `GROUP BY` → combines rows into one row
- `OVER()` → keeps all rows and adds calculated values

---

## Syntax

```sql
SELECT column_name,
       function_name() OVER()
FROM table_name;
```

---

## Example Table

Employee table:

| emp_id | fname    | salary |
|-------|----------|--------|
| 1     | Akanksha | 45000  |
| 2     | Rahul    | 50000  |
| 3     | Priya    | 60000  |

---

## Example 1: Average Salary

```sql
SELECT 
    fname,
    salary,
    AVG(salary) OVER() AS avg_salary
FROM employee;
```

Output:

| fname    | salary | avg_salary |
|---------|--------|-----------|
| Akanksha | 45000 | 51666 |
| Rahul    | 50000 | 51666 |
| Priya    | 60000 | 51666 |

Explanation:
- Average calculated once
- shown for every row

---

## Example 2: Sum of Salaries

```sql
SELECT
    fname,
    salary,
    SUM(salary) OVER() AS total_salary
FROM employee;
```

Output:

| fname | salary | total_salary |
|---|---|---|
| Akanksha | 45000 | 155000 |

---

## PARTITION BY

Divides rows into groups.

Similar to GROUP BY, but keeps rows.

---

## Example 3: Department Wise Average

```sql
SELECT
    fname,
    department,
    salary,
    AVG(salary) OVER(PARTITION BY department) AS dept_avg
FROM employee;
```

Output:

| fname | department | salary | dept_avg |
|---|---|---|---|
| Rahul | IT | 50000 | 55000 |
| Priya | IT | 60000 | 55000 |

---

## ORDER BY in OVER

Used for ranking or running totals.

---

## Example 4: Row Number

```sql
SELECT
    fname,
    salary,
    ROW_NUMBER() OVER(ORDER BY salary DESC) AS rank
FROM employee;
```

Output:

| fname | salary | rank |
|---|---|---|
| Priya | 60000 | 1 |
| Rahul | 50000 | 2 |
| Akanksha | 45000 | 3 |

---

## Example 5: Running Total

```sql
SELECT
    fname,
    salary,
    SUM(salary) OVER(ORDER BY emp_id) AS running_total
FROM employee;
```

Output:

| fname | running_total |
|---|---|
| Akanksha | 45000 |
| Rahul | 95000 |
| Priya | 155000 |

---

## Common Window Functions

- `ROW_NUMBER()`
- `RANK()`
- `DENSE_RANK()`
- `SUM()`
- `AVG()`
- `COUNT()`
- `MIN()`
- `MAX()`

---

## Why Use OVER?

- ranking
- running totals
- averages
- analytics
- reporting

---

## GROUP BY vs OVER

| GROUP BY | OVER |
|---|---|
| Groups rows | Keeps rows |
| One result per group | Result for each row |

Example:

GROUP BY:
```sql
SELECT department, AVG(salary)
FROM employee
GROUP BY department;
```

OVER:
```sql
SELECT fname, AVG(salary) OVER()
FROM employee;
```

---

## Summary

`OVER()` is used with window functions to perform calculations across rows while preserving original rows.

Useful for:
- analytics
- ranking
- cumulative totals
- reporting

---
