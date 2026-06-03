# Lab 05 — User ID Controlled by Request Parameter (IDOR)
**Date:** May 29, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
App uses a user ID in the URL to load account data — any user can change that ID to access someone else's account.

## How it works
- Logged in user's account page loads via URL like `/my-account?id=wiener`
- The server returns whatever account matches the ID in the URL
- No check that the logged in user actually owns that account

## How I found it
- Noticed the user ID in the URL when viewing my own account
- Swapped my username for carlos in the URL
- Server handed over his full account page including his API key

## What was exposed
Full account access for carlos including his API key

## Key lesson
This is called an Insecure Direct Object Reference (IDOR) — one of the most common access control vulnerabilities. The server exposed internal data based on a user supplied value without verifying ownership.

## Fix
Server must verify that the currently logged in user owns the resource they're requesting, not just serve whatever ID is in the URL.
