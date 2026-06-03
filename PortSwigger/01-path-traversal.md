# Lab 01 — Path Traversal (Simple Case)
**Date:** May 28, 2026  
**Platform:** PortSwigger Web Security Academy  
**Difficulty:** Apprentice  

## What it is
Manipulating a file path in a URL to escape the intended folder and access files elsewhere on the server.

## How it works
- App loaded images via `/image?filename=38.jpg`
- Server used the filename value directly with no checks
- `../` means "go up one folder" in Linux
- Chaining `../` sequences lets you climb to any folder on the server

## Payload used
`/image?filename=../../../etc/passwd`

## Tool used
Burp Suite Repeater — needed because the browser tried to render the response as an image instead of text

## What was exposed
`/etc/passwd` — f
