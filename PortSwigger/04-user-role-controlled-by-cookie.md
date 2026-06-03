# Lab 04 — User Role Controlled by Request Parameter
**Date:** May 28, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
Server grants admin access based on a client side cookie value that the user can freely edit.

## How it works
- Server sets `Admin=false` cookie on login
- Server trusts whatever cookie value the browser sends back
- Editing cookie to `Admin=true` grants full admin privileges

## How I found it
- DevTools → Application → Cookies
- Spotted a cookie named `Admin` with an obvious value of `false`

## Payload used
Changed cookie from `Admin=false` to `Admin=true`

## What was possible
Full admin panel access — deleted carlos

## Key lesson
Never trust the client. Anything stored in the browser can be edited by the user. Admin status must be verified server side, never based on a value the client sends.

## Fix
Store user roles server side tied to the session, never in an editable client side cookie.
