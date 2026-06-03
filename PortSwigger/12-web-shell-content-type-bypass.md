# Lab 12 — Web Shell Upload via Content-Type Restriction Bypass
**Date:** June 3, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
File upload that validates file type by checking the Content-Type header — which is user controllable and can be changed in Burp.

## How it works
- Server checks the Content-Type header to determine if the file is an image
- Content-Type header is sent by the browser and can be freely modified
- Changing it to `image/jpeg` tricks the server into accepting a PHP file

## How I did it
1. Uploaded `shell.php` through the avatar upload function
2. Intercepted the request in Burp
3. Changed `Content-Type: application/x-php` to `image/jpeg`
4. Forwarded the request — server accepted the file
5. Visited `/files/avatars/shell.php?cmd=cat+/home/carlos/secret`
6. Server executed the command and returned carlos' secret

## Key lesson
MIME type validation based on the Content-Type header is useless — it's sent by the browser and can be changed by anyone. Server must validate the actual file contents, not the header.

## Fix
Validate file type by reading the actual file contents server side, not the Content-Type header the client sends.
