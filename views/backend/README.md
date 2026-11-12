# Owl Core: Administrative Backend Views

Welcome to the administrative view architecture for **Owl Core**. This directory contains all presentation templates (`.gaze.php`) responsible for rendering the secure backend control panel, management dashboards, user analytics, and system configurations.

---

## 📂 Directory Structure  

```text
views/
├── backend/
│   ├── layout.gaze.php          # Master wrapper containing sidebar, navbar, and container slots
│   ├── sidebar.gaze.php         # Navigation links for users, logs, settings, and stats
│   ├── header.gaze.php          # Admin profile dropdown, live clock, and quick action triggers
│   └── footer.gaze.php          # Admin panel scripts, chart initializers, and asset bundles
│   └── dashboard.gaze.php           # Main metrics overview (Active sessions, user counts, system health)
│   └── edit.gaze.php            # Individual user record modification form


 🛠️ Core Conventions & Standards
1. View Extension (.gaze.php)
All administrative views use the .gaze.php extension, processed securely by the framework's rendering engine. Direct script execution is blocked at the core level via strict entry checks:

PHP
defined('ROOTPATH') OR die("Direct access denied.");
2. Layout Inheritance via Output Buffering
 
<div class="admin-dashboard-wrapper">
    <h1>System Overview</h1>
    <div class="metrics-grid">
        <div class="card">
            <h3>Active Sessions</h3>
            <p class="stat"><?= $active_users_count ?? 0; ?></p>
        </div>
    </div>
</div>
 
3. Flash Notifications & Alerts
Owl Core features a built-in global flash message helper. Instead of writing conditional HTML checks for success or error states across different admin forms, simply invoke:

PHP
<?php show_alerts(); ?>
This automatically sanitizes and outputs flash notices using standardized CSS classes (.alertsuccess and .alerterror).
 