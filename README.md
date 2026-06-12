# DBS101 – Database Systems:
# NOTES

## Table of Contents

- [Unit 1: Introduction to Database Systems](#unit-1-introduction-to-database-systems)
- [Unit 2: Database Design](#unit-2-database-design)
- [Unit 3: Introduction to SQL](#unit-3-introduction-to-sql)
- [Unit 5: Relational Database Design](#unit-5-relational-database-design)
- [Unit 6: Indexing and Query Processing](#unit-6-indexing-and-query-processing)

# Unit 1: Introduction to Database Systems

## What is a Database?
A structured collection of related data stored electronically and managed using a **DBS** (Database Management System).

- **Data** = raw facts (names, numbers, records)
- Organized data becomes **information**

## 3 Levels of Data Abstraction

| Level | Description |
|-------|-------------|
| **Physical** | How data is actually stored (files, indexes, storage formats) |
| **Logical** | What data is stored and relationships between them |
| **View** | What specific users see (hides unnecessary details) |


## Purpose of Database Systems

- Reduce data **redundancy**
- Ensure data **consistency**
- Allow data **sharing** among multiple users
- Enforce data **integrity** and **security**
- Provide **backup and recovery**


## History of Database Systems

| Era | Model |
|-----|-------|
| 1950s–60s | File Systems (separate files per app, lots of redundancy) |
| 1960s | Hierarchical DB (tree structure, one parent) — e.g. IBM IMS |
| 1970s | Network DB (multiple parents) — e.g. CODASYL |
| 1970s–Now | **Relational DB** (tables/relations, SQL) — proposed by Edgar F. Codd |
| Modern | NoSQL, Cloud, Distributed, Object-oriented DBs |


## Database Languages

| Language | Full Form | Commands |
|----------|-----------|----------|
| **DDL** | Data Definition Language | `CREATE`, `ALTER`, `DROP` |
| **DML** | Data Manipulation Language | `INSERT`, `UPDATE`, `DELETE`, `SELECT` |
| **DCL** | Data Control Language | `GRANT`, `REVOKE` |
| **TCL** | Transaction Control Language | `COMMIT`, `ROLLBACK` |


## Database Design Stages

1. **Conceptual** — ER diagram (entities & relationships)
2. **Logical** — Convert to relational tables
3. **Physical** — How data is stored (indexing, storage structures)


## ACID Properties

| Property | Meaning |
|----------|---------|
| **Atomicity** | All or nothing — transaction fully completes or fully rolls back |
| **Consistency** | DB always moves from one valid state to another |
| **Isolation** | Concurrent transactions don't interfere with each other |
| **Durability** | Committed data is permanently saved even after crashes |


## Database Architecture

| Tier | Description | Example |
|------|-------------|---------|
| **1-Tier** | App + DB on same machine | MS Access on a PC |
| **2-Tier** | Client connects directly to DB server | Desktop app + SQL Server |
| **3-Tier** | UI → Application → Database | Web browser → Web server → DB |


## Database Users

| User Type | Role |
|-----------|------|
| **DBA** | Manages security, backup, performance, user access |
| **Application Programmers** | Build apps that interact with the DB |
| **Sophisticated Users** | Write complex SQL queries |
| **End Users** | Use apps that access the DB |


# Unit 2: Database Design

## Design Process (5 Stages)

1. **Requirements Collection & Analysis** — identify data needs, business rules, stakeholders
2. **Conceptual Design** — create ER diagram (independent of any DBMS)
3. **Logical Design** — convert ER to relational tables, assign keys, apply normalisation
4. **Physical Design** — decide storage structures, indexes, access paths
5. **Implementation** — build the actual database


## Relational Model Key Terms

| Term | Meaning | Example |
|------|---------|---------|
| **Relation** | A table | Student table |
| **Tuple** | A row | (101, Sonam, IT) |
| **Attribute** | A column | StudentID, Name |
| **Domain** | Allowed values for an attribute | Age: 0–120 |


## ER Model Components

- **Entity** — real-world object (e.g. Student, Course)
- **Attribute** — property of an entity (e.g. Name, Age)
- **Relationship** — association between entities (e.g. Student *enrolls* Course)

### ER Symbols

| Symbol | Meaning |
|--------|---------|
| Rectangle | Entity |
| Double Rectangle | Weak Entity |
| Diamond | Relationship |
| Ellipse | Attribute |
| Underlined Ellipse | Key Attribute |
| Double Ellipse | Multivalued Attribute |
| Dashed Ellipse | Derived Attribute |
| Double line to entity | Total Participation |


## Types of Attributes

| Type | Description | Example |
|------|-------------|---------|
| **Simple** | Cannot be divided | Age, StudentID |
| **Composite** | Can be broken into parts | Address → Street, City |
| **Multivalued** | Multiple values possible | Phone numbers |
| **Derived** | Calculated from another attribute | Age from DateOfBirth |


## Mapping Cardinalities

| Type | Meaning | Example |
|------|---------|---------|
| **1:1** | One to one | Person ↔ Passport |
| **1:N** | One to many | Department → Employees |
| **N:1** | Many to one | Students → Department |
| **M:N** | Many to many | Students ↔ Courses |

## Keys

| Key | Description |
|-----|-------------|
| **Primary Key** | Uniquely identifies a record; unique, not NULL, minimal |
| **Candidate Key** | Any attribute(s) that could be primary key |
| **Composite Key** | Primary key made of multiple attributes |


## ER → Relational Schema (Mapping Rules)

| ER Component | Maps To |
|---|---|
| Entity | Table |
| Relationship | Foreign key or separate table |
| Multivalued attribute | Separate table |
| Weak entity | Table with owner's primary key included |


## Extended ER (EER) Features

| Feature | Description | Example |
|---------|-------------|---------|
| **Specialization** | Superclass split into subclasses | Employee → Manager, Engineer |
| **Generalization** | Subclasses merged into superclass | Car + Truck → Vehicle |
| **Inheritance** | Subclass inherits superclass attributes | Manager inherits Employee's ID |
| **Category (Union)** | Entity belongs to multiple sets | Owner = Person OR Company |


# Unit 3: Introduction to SQL

## Types of SQL Commands

| Type | Full Form | Purpose | Example |
|------|-----------|---------|---------|
| **DDL** | Data Definition Language | Define structure | `CREATE`, `ALTER`, `DROP` |
| **DML** | Data Manipulation Language | Modify data | `INSERT`, `UPDATE`, `DELETE` |
| **DQL** | Data Query Language | Retrieve data | `SELECT` |
| **DCL** | Data Control Language | Control access | `GRANT`, `REVOKE` |


## DDL Commands

```sql
-- Create a table
CREATE TABLE Student (
  StudentID INT PRIMARY KEY,
  Name VARCHAR(50),
  Age INT
);

-- Add a column
ALTER TABLE Student ADD Email VARCHAR(100);

-- Delete a table
DROP TABLE Student;
```


## Constraints

| Constraint | Meaning |
|------------|---------|
| `PRIMARY KEY` | Unique + Not NULL |
| `FOREIGN KEY` | Links to another table |
| `NOT NULL` | No empty values allowed |
| `UNIQUE` | No duplicate values |


## Key SQL Clauses

```sql
-- Basic structure
SELECT column FROM table WHERE condition;

-- ORDER BY
SELECT Name, Age FROM Student ORDER BY Age DESC;

-- GROUP BY + HAVING
SELECT Age, COUNT(*) FROM Student
GROUP BY Age
HAVING COUNT(*) > 1;
```

## Filtering Operators

| Operator | Example |
|----------|---------|
| `AND` / `OR` / `NOT` | `WHERE Age > 18 AND Name = 'John'` |
| `LIKE` | `WHERE Name LIKE 'A%'` — names starting with A |
| `BETWEEN` | `WHERE Age BETWEEN 18 AND 20` |
| `IN` | `WHERE Age IN (18, 22)` |

> `%` = any number of characters | `_` = single character (in LIKE)


# Unit 5: Relational Database Design

## 5.1 Features of Good Relational Design

A relation should model **one coherent concept** — each fact stored in one place only.

- **Minimal redundancy** – no unnecessary repetition
- **No anomalies** – update, insertion, or deletion shouldn't break other data
- **Lossless-join decomposition** – original relation recoverable after splitting
- **Dependency preservation** – constraints checkable without expensive joins


## 5.2 Decomposition Using Functional Dependencies

Split a relation into smaller ones when redundancy or normal form violations exist.

- **Lossless join** – R₁ ⋈ R₂ = R (no extra rows)
- **Dependency preservation** – FDs still enforceable on decomposed relations separately


## 5.3 Normal Forms

### 1NF – Every cell must have one atomic value. No repeating groups.
```
 PhoneNumbers: "17111111, 17222222"
 One row per phone number
```

### 2NF – In 1NF + no partial dependency.
```
ENROLLMENT(StudentID, CourseID, StudentName, CourseName, Grade)
   StudentName depends only on StudentID — partial dependency!

 STUDENT(StudentID, StudentName)
   COURSE(CourseID, CourseName)
   ENROLLMENT(StudentID, CourseID, Grade)
```

### 3NF – In 2NF + no transitive dependency.
```
EMPLOYEE(EmpID, EmpName, DeptID, DeptName)
   EmpID → DeptID → DeptName — transitive!

EMPLOYEE(EmpID, EmpName, DeptID)
   DEPARTMENT(DeptID, DeptName)
```

### Normal Forms Summary

| Normal Form | Removes |
|-------------|---------|
| 1NF | Multivalued / non-atomic cells |
| 2NF | Partial dependencies |
| 3NF | Transitive dependencies |
| BCNF | Stronger 3NF — every determinant must be a superkey |
| 4NF | Multivalued dependencies |
| 5NF | Join dependencies |


## 5.4 Functional-Dependency Theory

**X → Y** means: if two tuples agree on X, they must agree on Y.

### Armstrong's Axioms

| Rule | Meaning |
|------|---------|
| Reflexivity | If Y ⊆ X, then X → Y |
| Augmentation | X → Y ⟹ XZ → YZ |
| Transitivity | X → Y and Y → Z ⟹ X → Z |

- **Attribute Closure (X⁺)** – all attributes determined by X; used to find candidate keys.
- **Canonical Cover** – minimal equivalent set of FDs with no redundancy.


## 5.5 Decomposition Algorithms

- **BCNF Algorithm** – Decompose until no FD violates BCNF. Lossless but may lose dependencies.
- **3NF Synthesis** – Compute canonical cover → create relation per FD → add candidate key if missing. Guarantees lossless join + dependency preservation + 3NF.


## 5.6 Multivalued Dependencies (MVDs)

**X →→ Y** – X determines a set of Y values independent of other attributes.

Example: `Student →→ Hobby` and `Student →→ Language` — storing together causes redundancy → requires **4NF**.


## 5.9 Database Design Process

| Stage | Description |
|-------|-------------|
| Requirements Analysis | Users, rules, data items |
| Conceptual Design | ER diagrams |
| Logical Design | Relational schema, keys |
| Schema Refinement | Normalisation |
| Physical Design | Indexes, storage |
| Security & Application | Access control, views |


## 5.10 Temporal Data

| Concept | Meaning |
|---------|---------|
| Valid time | When fact is true in the real world |
| Transaction time | When fact is stored in the DB |
| Bitemporal | Both stored |

```sql
EmployeeSalary(EmployeeID, Salary, StartDate, EndDate)
```

# Unit 6: Indexing and Query Processing

## 6.1 Basic Concepts of Indexing

**Indexing** speeds up data retrieval using a separate structure of key values + pointers to actual records.

- Without index → full table scan: **O(n)**
- With index → direct lookup: **O(log n)**


## 6.2 Indexing Structures

**Single-level** – simple sorted key-pointer list. Not efficient for large data.

**Multi-level** – index on top of index; reduces search space.

### B-Tree
- Self-balancing; data at all nodes; height = log_M(N)
- All leaf nodes at same level

### B+ Tree  (Used by most DBMS)
- **Internal nodes** – keys only (navigation)
- **Leaf nodes** – all keys + data pointers, linked as a list
- Supports sequential and range access

| Feature | B-Tree | B+ Tree |
|---------|--------|---------|
| Data pointers | All nodes | Leaf nodes only |
| Search | Slower | Faster |
| Sequential access | No | Yes (linked leaves) |
| Deletion | Complex | Easy |
| Used in | Search engines | Database indexing |

> MySQL, Oracle, PostgreSQL all use **B+ Tree**.

---

## 6.3 Ordered vs Unordered Indices

| Feature | Ordered Index | Unordered Index |
|---------|--------------|-----------------|
| Search | Fast | Slow |
| Insert | Slower | Fast |
| Range Query | Efficient | Inefficient |


## 6.4 Temporal and Spatial Indexing

- **Temporal** – time-based access (e.g., salary history)
- **Spatial** – location-based access (e.g., maps, GPS). Uses **R-trees** and **Quad-trees**.


## 6.5 Indexing for Search

| Search Type | Example |
|-------------|---------|
| Exact match | `WHERE Name = 'Sonam'` |
| Range query | `WHERE Age > 20` |
| Pattern match | `WHERE Name LIKE 'S%'` |

> Too many indexes slow down `INSERT`, `UPDATE`, and `DELETE`.


## 6.6 Query Processing

```
SQL Query → Parsing → Relational Algebra → Optimization → Execution → Result
```

1. **Parsing** – checks syntax, table/column existence
2. **Translation** – converts SQL to relational algebra (σ, π operations)
3. **Optimization** – picks cheapest plan (minimises disk I/O, CPU, memory)
4. **Execution** – runs plan, returns result

### Query Cost
Measured mainly by **disk I/O**. Minimising disk access = faster query.

### Join Strategies

| Strategy | How it works |
|----------|-------------|
| Nested Loop Join | Each row of A compared with every row of B |
| Hash Join | Hash table built on one relation, probed with other |
| Sort-Merge Join | Both tables sorted on join key, then merged |

*References: Silberschatz et al. (2019), Elmasri & Navathe (2016, 2021)*