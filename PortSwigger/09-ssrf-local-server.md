# Lab 09 — Basic SSRF Against the Local Server
**Date:** June 2, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
Server makes HTTP requests on behalf of the user — attacker redirects those requests to internal services that should never be publicly accessible.

## How it works
- Shop has a stock check feature that fetches data from an internal URL
- The URL being fetched is controlled by the user via a `stockApi` parameter
- Replaced the stock URL with `http://127.0.0.1/admin/delete?username=carlos`
- Server made the request from itself — admin page trusts requests from loopback (127.0.0.1)

## How I did it
- Intercepted the stock check request in Burp Repeater
- Replaced the `stockApi` value with `http://127.0.0.1/admin/delete?username=carlos`
- Server deleted carlos — confirmed by 302 response

## Why 127.0.0.1 worked
The admin page only allowed access from loopback — meaning the server itself. By using SSRF to make the server send the request, it appeared to come from 127.0.0.1 and was trusted.

## Key lesson
Servers trust requests coming from themselves. If an attacker can make the server fetch an arbitrary URL they can access internal services, admin panels, and backend APIs that are firewalled from the public internet.

## Fix
Validate and whitelist URLs the server is allowed to fetch — never allow user controlled input t
