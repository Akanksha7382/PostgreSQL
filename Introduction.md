# PostgreSQL Introduction

## What is PostgreSQL?

PostgreSQL is an open-source relational database management system (RDBMS) used to store, manage, and retrieve data efficiently.

It is commonly used in:
- Web applications
- Data analytics
- Enterprise systems
- Backend development

PostgreSQL is known for:
- Reliability
- Scalability
- Advanced SQL support
- Strong data integrity

---

## Why Learn PostgreSQL?

PostgreSQL is widely used because it offers:

- Open source and free
- ACID compliance
- Advanced SQL features
- JSON support
- Indexing
- Views
- Stored Procedures
- Triggers
- Extensions

---

## Key Features

### 1. Relational Database
Stores data in tables with rows and columns.

Example:

| emp_id | name     | salary |
|--------|----------|--------|
| 1      | Akanksha | 45000  |

---

### 2. SQL Support
Supports SQL commands like:

```sql
SELECT * FROM employee;
INSERT INTO employee VALUES (...);
UPDATE employee SET salary = 50000;
DELETE FROM employee;
```

---

### 3. ACID Properties

PostgreSQL follows ACID:

- **Atomicity** → transaction fully completes or rolls back
- **Consistency** → valid data only
- **Isolation** → transactions do not interfere
- **Durability** → saved data remains permanent

---

### 4. Data Types

Common PostgreSQL data types:

- INTEGER
- VARCHAR
- TEXT
- DATE
- BOOLEAN
- NUMERIC
- SERIAL
- JSONB

Example:

```sql
salary NUMERIC(10,2)
```

---

### 5. Auto Increment with SERIAL

```sql
emp_id SERIAL PRIMARY KEY
```

Automatically generates:
1, 2, 3, 4...

---

## PostgreSQL Architecture

PostgreSQL contains:

- Database
- Schema
- Tables
- Views
- Functions
- Triggers
- Indexes

Structure:

```text
Database
 └── Schema
      └── Tables
```

---

## Difference Between MySQL and PostgreSQL

| MySQL | PostgreSQL |
|------|------------|
| Beginner friendly | Advanced features |
| Faster simple queries | Better complex queries |
| Basic JSON | JSONB support |

---

## Where PostgreSQL is Used

Companies using PostgreSQL:
- Instagram
- Spotify
- Reddit
- Netflix

---

## Summary

PostgreSQL is a powerful database system used for:
- storing data
- managing relationships
- running queries
- building scalable applications

It is one of the best databases for backend developers and data professionals.

---
