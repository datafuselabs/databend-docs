---
title: ASSUME_NOT_NULL
---

Results in an equivalent non-`Nullable` value for a Nullable type. In case the original value is `NULL` the result is undetermined. 

## Syntax

```sql
ASSUME_NOT_NULL(<x>)
```

## Aliases

- [REMOVE_NULLABLE](remove-nullable.md)

## Return Type

Returns the original datatype from the non-`Nullable` type; Returns the embedded non-`Nullable` datatype for `Nullable` type.

## Examples

```sql
CREATE TABLE default.t_null ( x int,  y int null);

INSERT INTO default.t_null values (1, null), (2, 3);

SELECT ASSUME_NOT_NULL(y), REMOVE_NULLABLE(y) FROM t_null;

┌─────────────────────────────────────────┐
│ assume_not_null(y) │ remove_nullable(y) │
├────────────────────┼────────────────────┤
│                  0 │                  0 │
│                  3 │                  3 │
└─────────────────────────────────────────┘
```