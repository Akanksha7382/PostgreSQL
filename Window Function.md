# Window Functions in PostgreSQL

## What are Window Functions?

Window functions perform calculations across a set of rows related to the current row **without collapsing rows**.

Unlike `GROUP BY`, window functions keep all original rows.

Used for:
- ranking
- running totals
- averages
- analytics reports

---

## Syntax

```sql
SELECT column_name,
       window_function() OVER()
FROM table_name;
```

General form:

```sql
function_name() OVER (
    PARTITION BY column_name
    ORDER BY column_name
)
```

---

## Example Table

Employee:

| emp_id | fname    | salary | department |
|-------|----------|--------|-----------|
| 1 | Akanksha | 45000 | HR |
| 2 | Rahul | 50000 | IT |
| 3 | Priya | 60000 | IT |
| 4 | Sneha | 40000 | HR |

---

## 1. ROW_NUMBER()

Assigns unique number to each row.

```sql
SELECT
    fname,
    salary,
    ROW_NUMBER() OVER(ORDER BY salary DESC) AS row_num
FROM employee;
```

Output:

| fname | salary | row_num |
|---|---|---|
| Priya | 60000 | 1 |
| Rahul | 50000 | 2 |
| Akanksha | 45000 | 3 |

---

## 2. RANK()

Assigns rank with gaps for ties.

```sql
SELECT
    fname,
    salary,
    RANK() OVER(ORDER BY salary DESC) AS rank
FROM employee;
```

Example:

| salary | rank |
|---|---|
| 60000 | 1 |
| 50000 | 2 |
| 50000 | 2 |
| 40000 | 4 |

Notice:
- rank 3 skipped

---

## 3. DENSE_RANK()

Same as rank but no gaps.

```sql
SELECT
    fname,
    salary,
    DENSE_RANK() OVER(ORDER BY salary DESC) AS rank
FROM employee;
```

Output:

| salary | rank |
|---|---|
| 60000 | 1 |
| 50000 | 2 |
| 50000 | 2 |
| 40000 | 3 |

---

## 4. NTILE()

Divides rows into groups.

```sql
SELECT
    fname,
    salary,
    NTILE(2) OVER(ORDER BY salary DESC) AS bucket
FROM employee;
```

Splits rows into 2 buckets.

---

## 5. LEAD()

Shows next row value.

```sql
SELECT
    fname,
    salary,
    LEAD(salary) OVER(ORDER BY salary) AS next_salary
FROM employee;
```

---

## 6. LAG()

Shows previous row value.

```sql
SELECT
    fname,
    salary,
    LAG(salary) OVER(ORDER BY salary) AS prev_salary
FROM employee;
```

---

## 7. SUM()

Running total.

```sql
SELECT
    fname,
    salary,
    SUM(salary) OVER(ORDER BY emp_id) AS running_total
FROM employee;
```

---

## 8. AVG()

Average across rows.

```sql
SELECT
    fname,
    salary,
    AVG(salary) OVER() AS avg_salary
FROM employee;
```

---

## PARTITION BY

Creates groups while keeping rows.

```sql
SELECT
    fname,
    department,
    salary,
    AVG(salary) OVER(PARTITION BY department) AS dept_avg
FROM employee;
```

Output:
- department-wise average

---

## ORDER BY in Window Function

Controls calculation order.

Example:

```sql
ORDER BY salary DESC
```

Used in:
- ranking
- cumulative sums

---

## Window Functions vs GROUP BY

| GROUP BY | Window Function |
|---|---|
| Collapses rows | Keeps rows |
| One result per group | Result per row |

GROUP BY:

```sql
SELECT department, AVG(salary)
FROM employee
GROUP BY department;
```

Window:

```sql
SELECT fname, AVG(salary) OVER()
FROM employee;
```

---

## Real Use Cases

- Salary ranking
- Top N employees
- Running totals
- Compare current vs previous row
- Analytics dashboards

---

## Summary

Common window functions:

- ROW_NUMBER()
- RANK()
- DENSE_RANK()
- NTILE()
- LEAD()
- LAG()
- SUM()
- AVG()

Window functions are powerful tools for analytics and reporting in PostgreSQL.

---
