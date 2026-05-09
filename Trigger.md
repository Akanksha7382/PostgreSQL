# Triggers in PostgreSQL

## What is Trigger?

A trigger is a database object that automatically executes a function when a specific event occurs on a table.

Events:
- INSERT
- UPDATE
- DELETE

Think of it like:

```text
If event happens → automatically perform action
```

Example:
- new employee added → log entry created
- salary updated → save previous salary
- row deleted → backup record

---

## Why Use Triggers?

Triggers are used for:

- automation
- auditing
- logging
- validation
- enforcing business rules

---

## Trigger Workflow

A trigger needs:

1. Trigger function
2. Trigger

Flow:

```text
Event occurs
   ↓
Trigger activates
   ↓
Function executes
```

---

## Syntax

### Step 1: Create Function

```sql
CREATE OR REPLACE FUNCTION function_name()
RETURNS TRIGGER AS $$
BEGIN
   logic
   RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

---

### Step 2: Create Trigger

```sql
CREATE TRIGGER trigger_name
AFTER INSERT
ON table_name
FOR EACH ROW
EXECUTE FUNCTION function_name();
```

---

## Example 1: Insert Trigger

Create function:

```sql
CREATE OR REPLACE FUNCTION log_insert()
RETURNS TRIGGER AS $$
BEGIN
   RAISE NOTICE 'New student inserted';
   RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

Create trigger:

```sql
CREATE TRIGGER student_insert_trigger
AFTER INSERT
ON students
FOR EACH ROW
EXECUTE FUNCTION log_insert();
```

Insert:

```sql
INSERT INTO students(name)
VALUES ('Riya');
```

Output:

```text
NOTICE: New student inserted
```

---

## BEFORE Trigger

Runs before event.

Example:
- validate salary before insert

```sql
CREATE TRIGGER trigger_name
BEFORE INSERT
ON employee
FOR EACH ROW
EXECUTE FUNCTION function_name();
```

Use cases:
- validation
- modify incoming data

---

## AFTER Trigger

Runs after event.

Example:
- logging
- audit trail

```sql
CREATE TRIGGER trigger_name
AFTER INSERT
ON employee
FOR EACH ROW
EXECUTE FUNCTION function_name();
```

---

## Example 2: Prevent Negative Salary

Function:

```sql
CREATE OR REPLACE FUNCTION check_salary()
RETURNS TRIGGER AS $$
BEGIN
   IF NEW.salary < 0 THEN
      RAISE EXCEPTION 'Salary cannot be negative';
   END IF;

   RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

Trigger:

```sql
CREATE TRIGGER salary_validation
BEFORE INSERT
ON employee
FOR EACH ROW
EXECUTE FUNCTION check_salary();
```

Now:

```sql
INSERT INTO employee(fname, salary)
VALUES ('Rahul', -5000);
```

Output:

```text
ERROR: Salary cannot be negative
```

---

## Example 3: Delete Trigger

Function:

```sql
CREATE OR REPLACE FUNCTION delete_notice()
RETURNS TRIGGER AS $$
BEGIN
   RAISE NOTICE 'Row deleted';
   RETURN OLD;
END;
$$ LANGUAGE plpgsql;
```

Trigger:

```sql
CREATE TRIGGER delete_trigger
AFTER DELETE
ON students
FOR EACH ROW
EXECUTE FUNCTION delete_notice();
```

---

## OLD and NEW

Used inside triggers.

### NEW
New row data.

Example:

```sql
NEW.salary
```

Used in:
- INSERT
- UPDATE

---

### OLD
Old row data.

Example:

```sql
OLD.salary
```

Used in:
- UPDATE
- DELETE

---

## Drop Trigger

```sql
DROP TRIGGER trigger_name ON table_name;
```

Example:

```sql
DROP TRIGGER student_insert_trigger ON students;
```

---

## Trigger vs Stored Procedure

| Trigger | Procedure |
|---|---|
| Automatic | Manual |
| Event based | User called |
| INSERT/UPDATE/DELETE | CALL statement |

Procedure:

```sql
CALL add_student('Akanksha');
```

Trigger:

```text
INSERT happens → trigger runs automatically
```

---



## Summary

Triggers automatically execute functions when:
- INSERT
- UPDATE
- DELETE

Used for:
- automation
- validation
- logging
- auditing

Triggers make databases smarter and more automated.

---
