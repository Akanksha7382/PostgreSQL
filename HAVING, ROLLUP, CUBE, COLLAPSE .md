# GROUP BY Extensions: HAVING, ROLLUP, CUBE, COLLAPSE

## HAVING

`HAVING` is used to filter grouped data after `GROUP BY`.

Difference:

- `WHERE` filters rows before grouping
- `HAVING` filters groups after grouping

## Syntax

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

## Example

Count employees in each department and show only departments with more than 2 employees.

```sql
SELECT department, COUNT(*)
FROM employee
GROUP BY department
HAVING COUNT(*) > 2;
```

Output:

| department | count |
|-----------|------|
| IT        | 3    |

---

## ROLLUP

`ROLLUP` creates subtotal rows plus grand total.

Useful for reports.

## Syntax

```sql
SELECT column1, SUM(column2)
FROM table_name
GROUP BY ROLLUP(column1);
```

## Example

```sql
SELECT department, SUM(salary)
FROM employee
GROUP BY ROLLUP(department);
```

Output:

| department | sum |
|-----------|------|
| HR        | 30000 |
| IT        | 90000 |
| NULL      | 120000 |

Explanation:
- HR total
- IT total
- NULL = grand total

---

## CUBE

`CUBE` creates all possible subtotal combinations.

More powerful than ROLLUP.

## Syntax

```sql
SELECT col1, col2, SUM(value)
FROM table_name
GROUP BY CUBE(col1, col2);
```

## Example

```sql
SELECT department, gender, COUNT(*)
FROM employee
GROUP BY CUBE(department, gender);
```

This generates:

- department totals
- gender totals
- department + gender totals
- grand total

---

## COLLAPSE

There is **no standard SQL keyword called COLLAPSE** in PostgreSQL or MySQL.

You may be confusing it with:

- `CUBE`
- `ROLLUP`
- `GROUPING SETS`

Sometimes people informally say "collapse data" meaning aggregate or summarize data.

Example of collapsing data:

```sql
SELECT department, COUNT(*)
FROM employee
GROUP BY department;
```

This collapses multiple rows into grouped summary.

---

## GROUPING SETS

Allows custom grouping combinations.

## Example

```sql
SELECT department, gender, COUNT(*)
FROM employee
GROUP BY GROUPING SETS (
    (department),
    (gender),
    ()
);
```

This gives:
- department totals
- gender totals
- grand total

---

## Summary

| Feature | Use |
|--------|-----|
| WHERE | Filter rows |
| HAVING | Filter groups |
| ROLLUP | Subtotals + grand total |
| CUBE | All subtotal combinations |
| GROUPING SETS | Custom grouping |

---
