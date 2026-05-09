# Stored Procedure in PostgreSQL

## What is a Stored Procedure?

A stored procedure is a collection of SQL statements stored inside the database that can be executed whenever needed.

It helps:
- Reuse SQL code
- Reduce repeated queries
- Improve maintainability
- Perform business logic inside database

Think of it like:

```text
Function in programming = Stored Procedure in SQL
```

---

## Syntax

```sql
CREATE PROCEDURE procedure_name()
LANGUAGE SQL
AS $$
   SQL statements
$$;
```

Call procedure:

```sql
CALL procedure_name();
```

---

## Example 1: Simple Stored Procedure

Create procedure:

```sql
CREATE PROCEDURE show_students()
LANGUAGE SQL
AS $$
SELECT * FROM students;
$$;
```

Execute:

```sql
CALL show_students();
```

---

## Example 2: Insert Data Using Procedure

```sql
CREATE PROCEDURE add_student(
    p_name VARCHAR(100)
)
LANGUAGE SQL
AS $$
INSERT INTO students(name)
VALUES (p_name);
$$;
```

Execute:

```sql
CALL add_student('Riya');
```

Result:
- New student inserted automatically

---

## Example 3: Procedure with Multiple Parameters

```sql
CREATE PROCEDURE add_course(
    p_name VARCHAR(100),
    p_fee NUMERIC
)
LANGUAGE SQL
AS $$
INSERT INTO courses(name, fee)
VALUES (p_name, p_fee);
$$;
```

Execute:

```sql
CALL add_course('Python', 5000);
```

---

## Why Use Stored Procedures?

### 1. Code Reusability
Write once, use multiple times.

---

### 2. Better Performance
Procedure is stored inside database.

---

### 3. Security
Users can execute procedure without direct table access.

---

### 4. Business Logic
Can handle:
- salary calculation
- order processing
- enrollment logic

---

## Drop Procedure

```sql
DROP PROCEDURE show_students;
```

---

## Stored Procedure vs Function

| Stored Procedure | Function |
|---|---|
| Called using `CALL` | Used in `SELECT` |
| May not return value | Must return value |
| Performs operations | Performs calculations |

Example:

Procedure:

```sql
CALL add_student('Akanksha');
```

Function:

```sql
SELECT total_salary();
```

---

## Real-life Example

Instead of manually writing:

```sql
INSERT INTO students(name)
VALUES ('Akanksha');
```

Again and again.

Use:

```sql
CALL add_student('Akanksha');
```

Cleaner and reusable.

---

## Summary

Stored procedures are used to:
- automate SQL tasks
- organize logic
- improve performance
- reduce repetitive code

They are useful for large applications and backend systems.

---
