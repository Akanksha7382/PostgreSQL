# Common Table Expression (CTE) 

## What is CTE?

CTE stands for **Common Table Expression**.

A CTE is a temporary result set created using the `WITH` keyword that can be referenced inside a query.

It makes SQL:
- cleaner
- more readable
- easier to manage

Think of it like:

```text
Temporary named query
```

---

## Syntax

```sql
WITH cte_name AS (
    query
)
SELECT * FROM cte_name;
```

---

## Basic Example

```sql
WITH high_salary AS (
    SELECT *
    FROM employee
    WHERE salary > 40000
)
SELECT * FROM high_salary;
```

Explanation:
- first creates temporary table `high_salary`
- then selects from it

---

## Without CTE

Same query without CTE:

```sql
SELECT *
FROM (
    SELECT *
    FROM employee
    WHERE salary > 40000
) AS high_salary;
```

Works, but less readable.

CTE is cleaner.

---

## Example 2: Aggregation

```sql
WITH dept_salary AS (
    SELECT department, AVG(salary) AS avg_sal
    FROM employee
    GROUP BY department
)
SELECT *
FROM dept_salary
WHERE avg_sal > 45000;
```

Output:

| department | avg_sal |
|---|---|
| IT | 55000 |

---

## Multiple CTEs

You can create multiple CTEs.

```sql
WITH student_count AS (
    SELECT COUNT(*) AS total_students
    FROM students
),
course_count AS (
    SELECT COUNT(*) AS total_courses
    FROM courses
)
SELECT *
FROM student_count, course_count;
```

Output:

| total_students | total_courses |
|---|---|
| 5 | 5 |

---

## CTE with JOIN

```sql
WITH enroll_data AS (
    SELECT
        s.name AS student_name,
        c.name AS course_name
    FROM enrollment e
    JOIN students s ON e.s_id = s.s_id
    JOIN courses c ON e.c_id = c.c_id
)
SELECT *
FROM enroll_data;
```

Useful for complex joins.

---

## Recursive CTE

Used for hierarchical data.

Example:
- employee-manager hierarchy
- category trees

Syntax:

```sql
WITH RECURSIVE cte_name AS (
   query
   UNION ALL
   recursive_query
)
SELECT * FROM cte_name;
```

Example:

```sql
WITH RECURSIVE numbers AS (
    SELECT 1 AS num
    UNION ALL
    SELECT num + 1
    FROM numbers
    WHERE num < 5
)
SELECT * FROM numbers;
```

Output:

| num |
|---|
| 1 |
| 2 |
| 3 |
| 4 |
| 5 |

---

## Why Use CTE?

### 1. Better readability
Breaks large query into smaller parts.

---

### 2. Reusability
Reference same result multiple times.

---

### 3. Easier debugging
Check query section by section.

---

### 4. Recursive queries
Supports hierarchical logic.

---

## CTE vs Subquery

| CTE | Subquery |
|---|---|
| More readable | Can be messy |
| Reusable | Repeated code |
| Good for complex queries | Better for simple queries |

---

## Real-life Example

Instead of writing a huge query:

```text
SELECT ...
JOIN ...
GROUP BY ...
HAVING ...
```

Break into steps:

```text
WITH filtered_data AS (...)
WITH aggregated_data AS (...)
```

Cleaner and easier.

---

## Summary

CTE is a temporary named query created with `WITH`.

Used for:
- readability
- complex queries
- recursive queries
- reusable query logic

---
