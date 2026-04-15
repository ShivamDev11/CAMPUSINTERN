# 🎓 CampusIntern - Student Internship Management System

A comprehensive web-based platform for managing student internships, designed specifically for educational institutions following NEP (New Education Policy) for OJT (On-Job Training) management.

## 📋 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [System Requirements](#system-requirements)
- [Installation Guide](#installation-guide)
- [Database Setup](#database-setup)
- [Admin Configuration](#admin-configuration)
- [Department Structure](#department-structure)
- [User Guide](#user-guide)
- [Folder Structure](#folder-structure)
- [Security Features](#security-features)
- [Troubleshooting](#troubleshooting)
- [Support](#support)

## 🎯 Overview

CampusIntern is a role-based internship management system that allows:
- **Students** to submit internship applications with documents
- **Department Admins** to manage department-specific internships
- **Admins** to upload guidelines, approve/reject submissions, and provide feedback

### Key Highlights
- ✅ Department-wise data isolation
- ✅ Role-based access control
- ✅ Secure file upload system
- ✅ Real-time notifications
- ✅ SQLite database (no separate server required)

## ✨ Features

### For Students
- Submit internship applications with offer letters
- Upload completion certificates
- Track application status (Pending/Approved/Rejected)
- Download department-specific guidelines
- Receive feedback from admins
- View personal internship history

### For Admins
- Department-specific dashboard
- View filtered internship submissions
- Approve/Reject applications
- Upload department-specific guidelines
- Provide feedback to students
- Download student documents
- Filter submissions by status, year, date

### Security Features
- Session-based authentication
- CSRF protection
- XSS prevention
- SQL injection prevention (PDO)
- Secure file uploads with .htaccess
- Department-based access control

## 🛠 Technology Stack

| Component | Technology |
|-----------|------------|
| Backend | PHP 7.4+ |
| Database | SQLite 3 |
| Frontend | HTML5, CSS3, Bootstrap 5 |
| JavaScript | Vanilla JS, Bootstrap JS |
| Server | Apache/Nginx |
| File Storage | Local file system |

## 💻 System Requirements

### Server Requirements
- PHP 7.4 or higher
- SQLite 3 extension enabled
- PHP extensions: PDO, SQLite3, GD, FileInfo
- Apache/Nginx web server

### PHP Configuration
```ini
upload_max_filesize = 10M
post_max_size = 10M
max_execution_time = 300
max_input_time = 300
Client Requirements
Modern web browser (Chrome, Firefox, Edge, Safari)

JavaScript enabled

Internet connection

📥 Installation Guide
Step 1: Download & Extract
bash
# Download the project
unzip CampusIntern-V1.0.zip
cd CampusIntern-V1.0
Step 2: Upload to Server
Local Server (XAMPP/WAMP)
bash
# Copy to htdocs folder
cp -r CampusIntern-V1.0 /opt/lampp/htdocs/
InfinityFree/Remote Hosting
bash
# Use FTP client to upload all files to public_html/
Step 3: Set Permissions
bash
# For Linux/Unix servers
chmod 777 db/
chmod 777 db/db.sqlite
chmod 777 student/uploads/
chmod 777 student/uploads/guidelines/

# For Windows servers (set write permissions via FTP)
Step 4: Configure Database
bash
# Database file is already included at:
# db/db.sqlite

# No additional setup needed - SQLite is file-based
Step 5: Test Installation
text
1. Open browser and navigate to: http://localhost/CampusIntern-V1.0/
2. Should redirect to login page
3. Login with default admin credentials
🗄 Database Setup
Database File Location
text
CampusIntern-V1.0/db/db.sqlite
Database Schema
users table
sql
- id (PRIMARY KEY)
- uid (unique identifier)
- name
- email
- password
- role (admin/student)
- department_code
- year
- roll_number
- created_at
internships table
sql
- id (PRIMARY KEY)
- student_id (FOREIGN KEY)
- department_code
- company
- position
- duration
- work_mode
- type
- offer_letter
- completion_certificate
- status (pending/approved/rejected)
- feedback
- created_at
- updated_at
guidelines table
sql
- id (PRIMARY KEY)
- file_name
- original_name
- file_path
- department_code
- uploaded_by
- uploaded_at
- file_size
- is_active
departments table
sql
- id (PRIMARY KEY)
- code (e.g., bit, bcm, mcm)
- full_name (e.g., BSC-IT, BCOM, MCOM)
admin_departments table
sql
- id (PRIMARY KEY)
- admin_id (FOREIGN KEY)
- department_code (FOREIGN KEY)
👑 Admin Configuration
Default Admin Credentials
Admin Name	Email	Password	Department
Admin BCOM/MCOM	admin1@college.edu	123456	BCOM, MCOM
Admin BMM	admin2@college.edu	123456	BMM
Admin IT Department	admin3@college.edu	123456	BSC-IT, BVOC-SD, MSCBIGDATA
Admin Science Department	admin4@college.edu	123456	BSC Physics, BSC Chemistry, Plain BSC
Admin BIOTECH	admin5@college.edu	123456	BIOTECH
Adding New Admin
sql
-- 1. Insert into users table
INSERT INTO users (name, email, password, role, department_code) 
VALUES ('New Admin', 'admin@college.edu', 'hashed_password', 'admin', NULL);

-- 2. Assign departments in admin_departments
INSERT INTO admin_departments (admin_id, department_code) 
VALUES (last_insert_id(), 'bit');
🏛 Department Structure
Department Codes Mapping
Code	Full Name	Admin
bit	BSC-IT	IT Admin
bsd	BVOC-SD	IT Admin
mbd	MSCBIGDATA	IT Admin
bcm	BCOM	BCOM/MCOM Admin
mcm	MCOM	BCOM/MCOM Admin
bmm	BMM	BMM Admin
bsc	Plain BSC	Science Admin
bpy	BSC Physics	Science Admin
bch	BSC Chemistry	Science Admin
bth	BIOTECH	BIOTECH Admin
📖 User Guide
Student Registration
Navigate to auth/register.php

Fill in personal details

Select department and year

Enter roll number (format: 24BSD008)

Create password

Submit registration

Student Login & Submission
Login at auth/login.php

Go to dashboard

Click "Create Submission"

Fill internship details

Upload offer letter (PDF)

Submit for approval

Admin Login & Management
Login with admin credentials

Dashboard shows department-specific submissions

Use filters to sort data

Approve/Reject applications

Upload department guidelines (PDF)

Provide feedback to students

📁 Folder Structure
text
CampusIntern-V1.0/
├── admin/                    # Admin panel files
│   ├── dashboard.php        # Admin dashboard
│   ├── approve.php          # Approve/Reject handler
│   ├── feedback.php         # Feedback system
│   ├── upload_guidelines.php # Guidelines upload
│   ├── view_form.php        # View submissions
│   └── profile.php          # Admin profile
├── auth/                    # Authentication files
│   ├── login.php            # Login page
│   ├── register.php         # Student registration
│   ├── logout.php           # Logout handler
│   └── forgot_password.php  # Password recovery
├── student/                 # Student panel files
│   ├── dashboard.php        # Student dashboard
│   ├── internship_form.php  # Submit internship
│   └── profile.php          # Student profile
├── includes/               # Core files
│   ├── config.php          # Database config
│   ├── header.php          # Site header
│   ├── footer.php          # Site footer
│   └── auth.php            # Auth functions
├── db/                     # Database
│   └── db.sqlite          # SQLite database
├── student/uploads/        # Uploaded files
│   └── guidelines/        # Guidelines PDFs
└── assets/                # Static assets
    └── images/            # Logo and images
🔒 Security Features
Implemented Security Measures
Authentication: Session-based login system

Authorization: Role-based access control (RBAC)

CSRF Protection: Tokens on all forms

XSS Prevention: htmlspecialchars() escaping

SQL Injection: PDO prepared statements

File Security: .htaccess to block direct access

Password Hashing: bcrypt for secure passwords

Session Security: Regenerate ID on login

HTTPS Ready: Compatible with SSL certificates

Security Headers
php
header("X-Frame-Options: DENY");
header("X-Content-Type-Options: nosniff");
header("Referrer-Policy: strict-origin-when-cross-origin");
header("Content-Security-Policy: default-src 'self'");
🐛 Troubleshooting
Common Issues & Solutions
Issue 1: Database Connection Error
text
Error: SQLSTATE[HY000]: General error: 8 attempt to write a readonly database
Solution:

bash
chmod 777 db/
chmod 777 db/db.sqlite
Issue 2: File Upload Fails
text
Error: File size exceeds limit
Solution:

Check php.ini upload limits

Or edit .htaccess:

ini
php_value upload_max_filesize 10M
php_value post_max_size 10M
Issue 3: Session Not Working
text
Error: session_start(): Cannot start session
Solution:

Check session save path permissions

Clear browser cookies

Issue 4: 404 Error on Pages
text
Error: The requested resource was not found
Solution:

Check if .htaccess is working

Verify file paths in includes files

Debug Mode
To enable debug mode, add to config.php:

php
error_reporting(E_ALL);
ini_set('display_errors', 1);
📞 Support
Contact Information
Developer: CampusIntern Team

Email: support@campusintern.com

Documentation: /docs/ directory

Reporting Issues
When reporting issues, include:

PHP version: php -v

Server type (XAMPP/InfinityFree/etc.)

Error message (screenshot)

Steps to reproduce

Useful Commands
Check PHP Version
bash
php -v
Check SQLite
bash
php -m | grep sqlite
Backup Database
bash
cp db/db.sqlite db/db_backup_$(date +%Y%m%d).sqlite
