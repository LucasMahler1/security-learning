# Lab 13 — OS Command Injection, Simple Case
**Date:** June 3, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
User supplied input is passed directly to a shell command on the server without sanitisation — allowing extra commands to be injected and executed.

## How it works
- Stock checker passes productId and storeId directly to a shell command
- The `&` character chains two commands together in Linux
- Injecting `& whoami` into the storeId runs both the stock check and `whoami`

## How I did it
1. Intercepted the stock check request in Burp Repeater
2. Modified the storeId parameter to `1+%26+whoami`
3. Server ran both commands and returned both outputs
4. Current server user revealed as `peter-kOMUl4`

## Payload used
`storeId=1+%26+whoami`
- `%26` is URL encoded `&`
- `&` chains two commands together in Linux

## Key lesson
Never pass user input directly to shell commands. The `&` character lets attackers chain any command they want onto whatever the server is already running — giving full command execution.

## Fix
Never construct shell commands from user input. Use safe APIs that don't invoke a shell, whitelist allowed input values, and strip any special shell characters from user input.
