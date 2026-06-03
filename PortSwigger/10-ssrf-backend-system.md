# Lab 10 — Basic SSRF Against Another Back-End System
**Date:** June 2, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
SSRF vulnerability where the admin interface is hidden on an internal back-end server at an unknown IP within the `192.168.0.X` range on port 8080.

## How I did it
1. Visited a product, clicked Check stock, intercepted the request in Burp and sent to Intruder
2. Changed the `stockApi` parameter to `http://192.168.0.1:8080/admin` then highlighted the final octet (`1`) and clicked Add §
3. Set payload type to Numbers — From: 1, To: 255, Step: 1
4. Launched attack and sorted by Status column — looked for the single `200` response
5. Sent that winning request to Repeater
6. Changed only the path in the `stockApi` to `/admin/delete?username=carlos`
7. Sent — 302 confirmed carlos deleted

## Key lesson
When something works in Intruder send that exact row to Repeater and modify minimally — don't rebuild the request from scratch as encoding errors will creep in.

Internal networks are not safe just because they aren't directly exposed to the internet. If any public facing feature can be redirected to make internal requests, the entire internal network becomes potentially accessible.

## Fix
Whitelist allowed URLs the server can fetch — block requests to internal IP ranges like `192.168.0.x`, `127.0.0.1`, and `10.x.x.x`.
