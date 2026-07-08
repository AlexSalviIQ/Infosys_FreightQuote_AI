# Intelligent Freight Quote Generation - Authentication Module (Milestone 1)

## 📌 Project Overview
This repository contains the core authentication and user management module for the **Intelligent Freight Quote Generation** platform. Built with Python and Streamlit, it provides a highly secure, responsive, and role-based access system designed to run seamlessly via Google Colab and Ngrok.

## ✨ Key Features
* **Secure User Registration:** Enforces strict password complexity rules (uppercase, lowercase, numbers, symbols, min 8 characters) and prevents duplicate email/username registrations.
* **Encrypted Authentication:** Utilizes `bcrypt` for secure password hashing and `PyJWT` (JSON Web Tokens) for stable session management.
* **Dual-Method Password Recovery:** * **Security Questions:** Instant reset using user-defined security answers.
  * **OTP Email Verification:** Sends a time-sensitive, 6-digit One-Time Password to the user's registered email using `smtplib`.
* **Role-Based Dashboards:** * **Admin Panel:** Exclusive root access (`admin@infosys.com`) to monitor all registered network operators.
  * **Operator Dashboard:** Provides system metrics, document indexing stats, and active task tracking for standard users.
* **Dynamic Enterprise UI:** Custom CSS overrides providing a sleek dark/light mode experience with responsive card containers and hidden default Streamlit branding.

## 🛠️ Technology Stack
* **Frontend:** Streamlit, HTML/CSS (Custom Styling)
* **Backend:** Python 3
* **Database:** SQLite3 (Local file-based database)
* **Security:** bcrypt, PyJWT, Python `secrets` module
* **Deployment/Hosting:** Google Colab, Pyngrok

## 🚀 How to Run the Application (Google Colab)
This application is designed to be executed in a Google Colab environment and exposed to the web using Ngrok.

### 1. Prerequisites
You will need to add two secret keys to your Google Colab **Secrets tab** (the key icon on the left sidebar):
* `NGROK_AUTHTOKEN`: Your personal authentication token from Ngrok.
* `EMAIL_PASSWORD`: A 16-character Google App Password used to send OTP emails.

### 2. Execution Steps
1. Open the notebook file in Google Colab.
2. Run the **Installation Cell** to install required dependencies:
   ```bash
   !pip install streamlit pyngrok bcrypt PyJWT
   ```
3. Run the **Application Cell** (`%%writefile app.py`) to generate the core script.
4. Run the **Server Cell** to launch the Streamlit server in the background and establish the Ngrok tunnel.
5. Click the generated `*.ngrok-free.dev` URL in the output to access the live application.

## 📁 Repository Structure
```text
├── app.py                  # Main application script
├── README.md               # Project documentation
└── screenshots/            # Directory containing visual proof of work
    ├── login_page.png
    ├── signup_validation.png
    ├── forgot_password_otp.png
    ├── email_inbox_otp.png
    ├── operator_dashboard.png
    └── admin_dashboard.png
```

*(Image: `screenshots/admin_dashboard.png`)*
