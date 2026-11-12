Markdown
# Owl Core: Authentication Request Handlers

Welcome to the request logic directory for **Owl Core**. This folder contains the backend action processors (`.catch.php`) responsible for handling incoming HTTP form submissions, validating credentials, managing authentication states, and executing user workflows.

---

## 📂 Directory Structure

```text
app/Requests/auth/
├── login.catch.php      # Processes authentication credentials, password verification, and session creation
├── register.catch.php   # Handles new user account validation, hashing, and database persistence
├── logout.catch.php     # Destroys active user sessions and clears security tokens
└── recovery.catch.php   # Manages password reset token generation and dispatch flows

🛠️ Core Conventions & Guidelines
1. File Naming & Extension (.catch.php)
All request logic files use the .catch.php suffix. They act as dedicated endpoint handlers mapped directly from routes to execute form logic without bloating controller classes.

Every request file must begin with the core security guard:

PHP
defined('ROOTPATH') OR die("Direct access denied.");
2. Request Lifecycle & Execution Pattern
Request handlers receive HTTP payloads ($_POST or $_GET), utilize auto-aliased models to query data, manage flash notifications, and handle redirection or JSON responses.

Example (app/Requests/auth/login.catch.php):

PHP
<?php
defined('ROOTPATH') OR die("Direct access denied.");

// 1. Validate request method
if ($_SERVER['REQUEST_METHOD'] !== 'POST') {
    Response::redirect('login');
}

// 2. Extract and sanitize input payload
$email = trim($_POST['email'] ?? '');
$password =$_POST['password'] ?? '';

🔐 Security Standards
CSRF Validation: Ensure incoming POST requests pass through token verification before processing credentials.

Input Sanitization: Always sanitize and validate raw input parameters before passing them into database query builders or ORM methods.