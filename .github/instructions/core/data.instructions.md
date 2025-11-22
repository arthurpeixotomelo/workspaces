---
description: 'Data modeling, database design, and SQL standards for all data-related files.'
applyTo: '**/*.{db,sql,duckdb,sqlite,parquet,pbix,json,txt,ddl,dml}'
---

# Data Architecture & Modeling

## Overview

This document provides comprehensive guidelines for data modeling, database design, and SQL development. It integrates principles from relational database design, dimensional modeling (Star Schema), and SQL best practices.

## Data Modeling Principles

### Star Schema (Dimensional Modeling)
- **Dimension Tables**: Store descriptive business entities (Products, Customers, Time). Use surrogate keys (integers/UUIDs). Keep them wide (many attributes) and shallow.
- **Fact Tables**: Store measurable events (Sales, Logs). Use foreign keys to dimensions and numeric measures. Keep them narrow and deep.
- **Relationships**: Prefer One-to-Many (Dimension -> Fact). Avoid Many-to-Many without bridge tables. Avoid Bi-directional filtering unless necessary.

### Normalization
- **Operational DBs**: Normalize to 3NF to reduce redundancy and ensure integrity.
- **Analytical/Reporting**: Denormalize (Star Schema) for read performance and simplicity.

### Naming Conventions
- **Tables**: Singular form (e.g., `customer`, `order`). Snake_case.
- **Columns**: Singular, snake_case. Clear and descriptive.
- **Keys**:
  - Primary Key: `id` (or `table_id` if preferred for clarity in joins, but be consistent).
  - Foreign Key: `referenced_table_id`.

## Database Standards

### Schema Design
- **Primary Keys**: Every table MUST have a primary key.
- **Audit Columns**: Include `created_at` and `updated_at` timestamps.
- **Constraints**: Use NOT NULL by default. Enforce referential integrity with Foreign Keys.
- **Indexing**: Index Foreign Keys and columns frequently used in WHERE/JOIN/ORDER BY. Avoid over-indexing.

### File Organization
- Place database files in `api/db/` (or equivalent data root).
- Subfolders: `migrations/`, `seeds/`, `schema/`.

## SQL Development

### Coding Style
- **Keywords**: Uppercase (SELECT, FROM, WHERE).
- **Indentation**: Consistent indentation for clauses.
- **Aliases**: Use meaningful aliases for tables in joins.

### Query Structure
- **Explicit Columns**: Always list columns in SELECT (No `SELECT *`).
- **Joins**: Prefer explicit JOIN syntax over implicit joins in WHERE.
- **SARGable**: Avoid functions on indexed columns in WHERE clauses.

### Stored Procedures (SQL Server/General)
- **Naming**: PascalCase, prefix with `usp_` (e.g., `usp_GetCustomerOrders`).
- **Parameters**: CamelCase, prefix with `@`.
- **Logic**:
  - Parameterize queries to prevent Injection.
  - Use `SET NOCOUNT ON` for performance.
  - Handle transactions explicitly (BEGIN/COMMIT/ROLLBACK).
  - Return standardized error codes/messages.

## Power BI & Analytical Specifics

### Date Tables
- Always use a dedicated Date dimension table.
- Mark as "Date Table" in model.
- Include standard hierarchy (Year > Quarter > Month > Day).

### Slowly Changing Dimensions (SCD)
- **Type 1 (Overwrite)**: For corrections/non-critical changes.
- **Type 2 (History)**: For tracking changes over time (EffectiveDate, ExpirationDate, IsCurrent).

### Performance
- **Import Mode**: Remove unused columns/rows. Optimize data types.
- **DirectQuery**: Optimize source DB indexes. Assume Referential Integrity if safe.
