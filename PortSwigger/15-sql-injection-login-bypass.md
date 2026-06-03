# Lab 15 — SQL Injection Login Bypass
**Date:** June 3, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
SQL injection in the login function — manipulating the query to bypass password authentication entirely.

## The vulnerable query
```sql
SELECT * FROM users WHERE username = 'administrator' AND password = 'anything'
```

## Payload used
- Username: `administrator'--`
- Password: anything

## What it did to the query
```sql
SELECT * FROM users WHERE username = 'administrator'--' AND password = 'anything'
```
- `'` — closed the username string early
- `--` — commented out the entire password check
- Database found the administrator user and logged in without verifying the password

## How I did it
1. Intercepted the login POST request in Burp Suite
2. Modified the username parameter to `administrator'--`
3. Forwarded the request — logged in as administrator with no password

## Key lesson
SQL injection in login forms can bypass authentication entirely — no password needed. The attacker doesn't need to know or crack the password, they just make the database ignore it.

## Fix
Use parameterised queries — these ensure user input is always treated as plain data and never interpreted as SQL code. Never build login queries by concatenating user input directly.
