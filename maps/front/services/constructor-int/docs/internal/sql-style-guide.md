# SQL Style Guide

This document describes SQL style guide used in the project.

## Table of Contents

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Naming conventions](#naming-conventions)
  - [General](#general)
  - [Tables](#tables)
  - [Columns](#columns)
  - [Indexes](#indexes)
  - [Functions, triggers, procedures](#functions-triggers-procedures)
- [Query syntax](#query-syntax)
  - [Reserved words](#reserved-words)
  - [Functions](#functions)
  - [Types](#types)
  - [Spaces](#spaces)
  - [Single-line query](#single-line-query)
  - [Multi-line query](#multi-line-query)
- [Joins](#joins)
- [Inserts](#inserts)
- [Notes](#notes)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Naming conventions

### General

* Ensure the name is unique and does not exist as a [reserved keyword](https://www.postgresql.org/docs/9.5/static/sql-keywords-appendix.html).
* Names must begin with a letter and may not end with an underscore.
* Only use letters, numbers and underscores in names.
* Avoid abbreviations and if you have to use them make sure they are commonly understood.

### Tables

* Use `snake_case` style.
* Use a collective name, e.g. `maps` instead `map`.
* Do not prefix with `tbl_` or any other such descriptive prefix or Hungarian notation.

### Columns

* Use `snake_case` style.
* For primary key of the table use `id` name.
* For foreign keys of the table use `${singular table name}_id` style, e.g. `map_id` column in
  `objects` table which references to `id` column in `maps` table.
* Do not add a column with the same name as its table and vice versa.

### Indexes

* Use `snake_case` style.
* Start name with table name and end with `_index`, e.g. `maps_time_created_index` is an index for
  the `time_created` column of the `maps` table.

### Functions, triggers, procedures

* Use `snake_case` style.

## Query syntax

### Reserved words

Always use uppercase for the SQL keywords:

**Good:**

```sql
SELECT properties FROM maps WHERE sid = $1;
```

**Bad:**

```sql
select properties from maps where sid = $1;
```

### Functions

Always use lowercase for the SQL functions:

**Good:**

```sql
SELECT count(*) FROM maps;
```

**Bad:**

```sql
SELECT COUNT(*) FROM maps;
```

### Types

Always use lowercase for types:

**Good:**

```sql
CREATE TABLE foo (id bigserial PRIMARY KEY);
```

**Bad:**

```sql
CREATE TABLE foo (id BIGSERIAL PRIMARY KEY);
```

### Spaces

Use one space:

* before and after [comparison operators](https://www.postgresql.org/docs/9.5/static/functions-comparison.html)
* after commas (`,`)

**Good:**

```sql
SELECT properties, revision FROM maps WHERE sid = $1;
```

**Bad:**

```sql
SELECT properties,revision FROM maps WHERE sid=$1;
```

### Single-line query

Short query can be written in single line:

```sql
SELECT properties, state FROM maps WHERE sid = $1;
```

### Multi-line query

Long queries should be splitted into several lines with the following rules:

* Use `4` spaces for one indentation level.
* Each statement and clause should be placed on new line:

  ```sql
  SELECT
      maps.sid,
      maps.time_created,
      maps.time_updated,
      maps.properties,
      maps.options,
      maps.state,
      maps.revision
  FROM maps
  JOIN maps_users ON maps.id = maps_users.map_id
  WHERE maps_users.uid = $1
  ORDER BY maps.time_updated DESC
  LIMIT $2 OFFSET $3;
  ```

* Alignment should be avoided:

  **Bad:**

  ```sql
    SELECT properties, state
      FROM maps
     WHERE sid = $1
  ORDER BY time_updated DESC;
  ```

* Multi-line conditions should be written with one level indentation. Conditional operators should be
  placed after line break:

  ```sql
  SELECT
      sid,
      properties,
      options,
      state,
      revision
  FROM maps
  WHERE
      sid = $1
      AND deleted = FALSE
      AND (
          properties->>'access' = 'public'
          OR properties->>'access' = 'link'
      );
  ```

## Joins

* When join is used, column names should be qualified with corresponding table names:

  **Good:**

  ```sql
  SELECT
      maps.sid,
      maps_users.uid
  FROM maps
  JOIN maps_users ON maps.id = maps_users.map_id;
  ```

  **Bad:**

  ```sql
  SELECT
      sid,
      uid
  FROM maps
  JOIN maps_users ON maps.id = maps_users.map_id
  ```

## Inserts

* Always add a column definition list for INSERTs:

  > Explanation: If the table structure changes, your code might break in surprising ways.

  **Good:**

  ```sql
  INSERT INTO maps (sid, properties, options) VALUES ($1, $2, $3);
  ```

  **Bad:**

  ```sql
  INSERT INTO maps VALUES ($1, $2, $3);
  ```

## Notes

Structure of this document is based on http://www.sqlstyle.guide
