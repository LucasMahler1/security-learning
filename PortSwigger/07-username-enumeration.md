# Lab 07 — Username Enumeration via Different Responses
**Date:** May 29, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
Login page gives different error messages for invalid usernames vs wrong passwords — leaking which usernames exist on the system.

## How it works
- "Invalid username" = username doesn't exist
- "Incorrect password" = username IS valid, password is wrong
- That difference lets an attacker enumerate valid usernames then brute force the password

## How I did it
1. Captured login request in Burp → sent to Intruder
2. Set username as payload position, loaded candidate usernames wordlist
3. Found `ao` — its response said "Incorrect password" instead of "Invalid username"
4. Switched payload to password field with `ao` as fixed username
5. Loaded candidate passwords wordlist
6. Found `112233` — different response length indicated successful login

## Tools used
Burp Suite Intruder — automated hundreds of login attempts using wordlists

## Key lesson
Error messages leak information. A login page should always return the exact same message whether the username or password is wrong — something generic like "Invalid username or password".

## Fix
Use identical error messages for all failed login attempts. Also implement rate limiting and account lockout to prevent automated brute force attacks.
