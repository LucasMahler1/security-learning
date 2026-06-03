# Lab 11 — Remote Code Execution via Web Shell Upload
**Date:** June 2, 2026
**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice

## What it is
File upload function with no validation — accepts any file type including executable PHP scripts.

## How it works
- App allows avatar image uploads with zero file type checking
- Uploaded a PHP web shell disguised as an avatar
- Server stored and executed it as PHP code
- Used the shell to run arbitrary commands on the server

## The web shell used
```php
<?php system($_GET['cmd']); ?>
```

## How I did it
1. Logged in as wiener:peter
2. Created `shell.php` containing the web shell one liner
3. Uploaded it through the avatar upload function
4. Found storage path via Inspect — `/files/avatars/shell.php`
5. Visited URL with `?cmd=cat+/home/carlos/secret`
6. Server executed the command and returned carlos' secret

## Key lesson
Never trust file uploads. Accepting a file and storing it on the server without validation is one of the most dangerous vulnerabilities — it can lead to full remote code execution.

## Fix
Validate file type server side, rename uploaded files, store them outside the web root so they can't be executed, and never allow uploaded files to be served as executable code.
