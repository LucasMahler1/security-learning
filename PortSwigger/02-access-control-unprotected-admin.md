# Lab 02 — Unprotected Admin Functionality
**Date:** May 28, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
An admin panel exposed publicly with no login or access control protecting it — anyone who finds the URL can use it.

## How it works
- Admin functionality hidden at `/administrator-panel`
- No authentication required to access it
- Once inside had full ability to delete users

## How I found it
- Checked `/robots.txt` — sites often list hidden paths there to tell search engines not to index them, accidentally revealing secret URLs to attackers

## What was possible
Full admin access — viewed all users and deleted one

## Fix
Always protect admin pages behind proper authentication and authorisation checks, even if the URL is not publicly linked anywhere. Security through obscurity is not real security.
