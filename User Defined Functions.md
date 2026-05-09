# User Defined Functions (UDF) in PostgreSQL

## What is User Defined Function?

A User Defined Function (UDF) is a custom function created by users to perform specific operations inside PostgreSQL.

It can:
- accept parameters
- process logic
- return a value

Think of it like:

```text
Python function = SQL User Defined Function
```

Example:

Python:
```python
def add(a, b):
    return a + b
```

PostgreSQL:
```sql
CREATE FUNCTION add_numbers(a INT, b INT)
RETURNS INT
AS $$
BEGIN
   RETURN a + b;
END;
$$ LANGUAGE plpgsql;
```

---

## Why Use Functions?

- Reusable logic
- Cleaner queries
- Avoid repeated calculations
- Business logic inside database

---

## Syntax

```sql
CREATE FUNCTION function_name(parameters)
RETURNS return_type
AS $$
BEGIN
   logic
END;
$$ LANGUAGE plpgsql;
```

Execute:

```sql
SELECT function_name();
```

---

## Example 1: Simple Function

```sql
CREATE FUNCTION get_message()
RETURNS TEXT
AS $$
BEGIN
   RETURN 'Hello PostgreSQL';
END;
$$ LANGUAGE plpgsql;
```

Run:

```sql
SELECT get_message();
```

Output:

```text
Hello PostgreSQL
```

---

## Example 2: Add Two Numbers

```sql
CREATE FUNCTION add_numbers(a INT, b INT)
RETURNS INT
AS $$
BEGIN
   RETURN a + b;
END;
$$ LANGUAGE plpgsql;
```

Run:

```sql
SELECT add_numbers(10, 20);
```

Output:

```text
30
```

---

## Example 3: Calculate Bonus

```sql
CREATE FUNCTION calculate_bonus(salary NUMERIC)
RETURNS NUMERIC
AS $$
BEGIN
   RETURN salary * 0.10;
END;
$$ LANGUAGE plpgsql;
```

Run:

```sql
SELECT calculate_bonus(50000);
```

Output:

```text
5000
```

---

## Example 4: Function with Table Data

```sql
CREATE FUNCTION total_students()
RETURNS INT
AS $$
DECLARE
   total INT;
BEGIN
   SELECT COUNT(*) INTO total
   FROM students;

   RETURN total;
END;
$$ LANGUAGE plpgsql;
```

Run:

```sql
SELECT total_students();
```

Output:

```text
5
```

---

## Function with Parameters

```sql
CREATE FUNCTION square_num(n INT)
RETURNS INT
AS $$
BEGIN
   RETURN n * n;
END;
$$ LANGUAGE plpgsql;
```

Run:

```sql
SELECT square_num(4);
```

Output:

```text
16
```

---

## Drop Function

```sql
DROP FUNCTION function_name;
```

Example:

```sql
DROP FUNCTION add_numbers;
```

---

## Function vs Procedure

| Function | Procedure |
|---|---|
| Must return value | Return optional |
| Used with SELECT | Used with CALL |
| Calculation logic | Business operations |

Function:

```sql
SELECT add_numbers(10,20);
```

Procedure:

```sql
CALL add_student('Akanksha');
```

---

## Real-life Example

Instead of repeatedly writing:

```sql
salary * 0.10
```

Create function:

```sql
SELECT calculate_bonus(50000);
```

Reusable and clean.

---

## Summary

User Defined Functions are custom functions created by users to:
- perform calculations
- reuse logic
- simplify SQL queries
- improve maintainability

---
