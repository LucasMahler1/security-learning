# Lab 06 — User ID Controlled by Request Parameter with Password Disclosure
**Date:** May 29, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
Account page prefills the user's password in a masked input field — the password is hidden visually but exposed in the page source.

## How it works
- Same IDOR as last lab — swapped `?id=wiener` to `?id=administrator` in the URL
- Server loaded the administrator's account page including their prefilled password field
- Browser displayed it as dots but the raw value was sitting in the HTML

## How I found it
- Changed the ID in the URL to administrator
- Right clicked the password field → Inspect
- Found the plaintext password sitting in the `value=` attribute of the input element
- Logged in as administrator and deleted carlos

## What was exposed
Administrator plaintext password — full account takeover

## Key lesson
Never send sensitive data to the browser that you don't want the user to see. Masking a password field only hides it visually — the value is still in the HTML and anyone can read it with DevTools.

## Fix
Never prefill password fields with real passwords. If users need to change their password, make them enter the current one manually — never send it from the server to the client.
