# Lab 03 — Unprotected Admin Functionality with Unpredictable URL
**Date:** May 28, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
Hidden admin panel at a randomised URL with no authentication — developer assumed nobody would find it.

## How it works
- Admin panel hidden at an unpredictable path like `/admin-i6eg6r`
- Developer thought an unguessable URL was enough protection
- URL was hardcoded in the page's JavaScript source code

## How I found it
- Opened DevTools → Sources → searched for "admin" across all files
- Found it hardcoded in a script tag on the index page

## What was possible
Full admin access — deleted user carlos

## Key lesson
Hiding a URL is not the same as securing it. Any JavaScript that runs in the browser is readable by anyone. Never put secret paths, credentials, or sensitive logic in client side code.

## Fix
Protect every admin route with proper server side authentication regardless of how obscure the URL is.
