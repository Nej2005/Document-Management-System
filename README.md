# Document Management System (DMS)

A web-based Document Management System developed for organizational use. The system enables users to securely upload, store, classify, encrypt, and manage documents, with support for role-based access, email notifications, and OCR-based document classification.

---

## Table of Contents

- [Features](#features)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Environment Configuration](#environment-configuration)
- [Running the Application](#running-the-application)
- [Project Structure](#project-structure)

---

## Features

- Secure document upload and storage
- Automatic document classification using OCR
- Fernet-based encryption for sensitive data
- Role-based access control
- Email notification system
- Support for multiple file formats (PDF, DOCX, XLSX, PPTX, images)

---

## Technology Stack

| Layer      | Technology                        |
|------------|-----------------------------------|
| Backend    | Python, Flask                     |
| Frontend   | HTML, CSS, JavaScript             |
| Database   | MySQL                             |
| Encryption | Python `cryptography` (Fernet)    |
| Email      | SMTP via Gmail                    |
| OCR        | `pdfplumber`, `pdf2image`, Pillow |

---

## Prerequisites

Ensure the following are installed on your machine before proceeding:

- **Python** 3.10 or higher — [python.org](https://www.python.org/downloads/)
- **MySQL Server** 8.0 or higher — [mysql.com](https://dev.mysql.com/downloads/)
- **pip** (comes bundled with Python)
- **Poppler** (required by `pdf2image` for PDF rendering)
  - Windows: Download from [poppler-windows](https://github.com/oschwartz10612/poppler-windows/releases) and add the `bin/` folder to your system `PATH`.

---

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Nej2005/Document-Management-System.git
cd Document-Management-System
```

### 2. Create a Virtual Environment (Recommended)

```bash
python -m venv venv
```

Activate the virtual environment:

- **Windows:**
  ```bash
  venv\Scripts\activate
  ```
- **macOS/Linux:**
  ```bash
  source venv/bin/activate
  ```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Set Up the Database

1. Open your MySQL client and create a new database:
   ```sql
   CREATE DATABASE dms_db;
   ```
2. Import the provided schema (if available) or allow the application to initialize the tables on first run.

---

## Environment Configuration

The application requires a `.env` file in the root directory to store sensitive credentials. This file is **not included in the repository** for security reasons.

Create a `.env` file in the project root with the following contents:

```env
# Fernet encryption key (generate using: python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())")
DMS_FERNET_KEY=your_fernet_key_here

# SMTP email configuration
smtp_server = smtp.gmail.com
smtp_port = 587
sender_email = your_email@gmail.com
sender_password = your_app_password_here
```

> **Note:** For `sender_password`, use a [Gmail App Password](https://support.google.com/accounts/answer/185833), not your regular Gmail password. Two-Factor Authentication must be enabled on the account.

To generate a new Fernet key, run:

```bash
python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())"
```

Refer to `FERNET_ENCRYPTION_GUIDE.md` for detailed instructions on encryption setup.

---

## Running the Application

Once the environment is configured, start the Flask development server:

```bash
python app.py
```

By default, the application runs at:

```
http://127.0.0.1:5000
```

Open `login.html` or navigate to the above URL in your browser to access the system.

---

## Project Structure

```
Document-Management-System/
├── app.py                      # Main Flask application
├── document_classifier.py      # OCR-based document classification
├── email_sender.py             # Email notification module
├── crypt.py                    # Encryption utilities
├── requirements.txt            # Python dependencies
├── .env                        # Environment variables (not committed)
├── .gitignore                  # Git ignore rules
├── database/                   # Database configuration and schema
├── uploads/                    # Uploaded documents (not committed)
├── OCR file type/              # OCR-related assets
├── login.html                  # Login page
├── app.html                    # Main application interface
└── FERNET_ENCRYPTION_GUIDE.md  # Encryption setup guide
```

---

## Important Notes

- The `.env` file contains sensitive credentials and must **never** be committed to version control.
- The `uploads/` directory stores user-uploaded files and is excluded from the repository.
- Ensure your MySQL server is running before starting the application.

---

*Developed as part of an academic project.*
