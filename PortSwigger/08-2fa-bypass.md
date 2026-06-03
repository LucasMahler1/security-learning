# Lab 08 — 2FA Simple Bypass
**Date:** June 1, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
Two factor authentication that can be skipped entirely by navigating directly to the post-login page.

## How I did it
- Logged into my own account first to identify the account page URL format
- Logged in as carlos with valid credentials
- When redirected to the 2FA page, manually navigated to `/my-account?id=carlos` instead
- Server never verified 2FA was completed — just served the account page

## Key lesson
2FA is only effective if the server enforces completion of every step before granting access. If the protected page is accessible directly via URL the entire 2FA layer is meaningless.

## Fix
Server must track authentication state — marking a session as fully authenticated only after 2FA is completed. Navigating directly to protected pages should redirect back to the 2FA step, not grant access.
