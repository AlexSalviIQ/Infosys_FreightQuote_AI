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
1. Go to [ngrok.com](https://ngrok.com/) and create a free account.
2. Once logged in, navigate to your dashboard.
3. On the left sidebar, expand **Getting Started** and click on **Your Authtoken**.
4. Click the **Copy** button to save your token.
5. In Google Colab, add a new secret named `NGROK_AUTHTOKEN` and paste this value.
* `EMAIL_PASSWORD`: A 16-character Google App Password used to send OTP emails.
1. Go to your [Google Account Security page](https://myaccount.google.com/security).
2. Scroll down to the **How you sign in to Google** section and ensure **2-Step Verification** is turned **ON**.
3. Click on **2-Step Verification**, scroll to the very bottom of the page, and click on **App Passwords**.
4. In the "App name" field, type a custom name (e.g., "Freight Portal Colab").
5. Click **Create**. Google will generate a 16-character password in a pop-up window. 
6. Copy this exact 16-character string (you can ignore the spaces). **Note: Google will only show you this password once.**
7. In Google Colab, add a new secret named `EMAIL_PASSWORD` and paste this 16-character string.

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

Login Page
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/cf699063-4eea-4891-bc9d-ebd9ca4bfec5" />
SignUp_Page: Wrong Email
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/147c458e-bce5-4f76-8f16-aa6fcf540467" />
SignUp_Page: Weak Password
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/14adef9f-91e6-4d8c-8aee-df826e34907d" />
SignUp_Page: No Security Questions’s Answer
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/bb231ab0-ffa3-41a9-8622-2437f9522f89" />
Dashboard Page(User)
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/194981aa-bf67-4cc9-9343-cd424baf79ba" />
Forget_Password Page
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/0f95c033-47b2-42a4-a3eb-e881d96b4d11" />
Forget_Password Page: Security Question
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/c80ae166-001c-4287-a977-ba1e2925bc06" />
Forget_Password Page: Incorrect Security Answer
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/9e9128c0-8ea6-498c-a02e-5931bc426547" />
Forget_Password Page: Successful Password Reset using Security Questions
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/5d877700-e4ef-4bce-b424-36a4fb9fa9f6" />
Forget_Password Page: via OTP
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/083047f5-2adf-4252-845f-ba44fadad609" />
Forget_Password Page: Invalid OTP
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/48a1a4a6-9750-4951-8982-124c4ebefb23" />

Gmail: OTP Recieved

<img width="525" height="665" alt="image" src="https://github.com/user-attachments/assets/378ba233-261b-42f7-ae61-3e2f6ec21bb8" />

Forgot_Password_Page: Successfully reset password through OTP
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/c9577feb-4d9b-4f2e-8ae9-030fdc0bffff" />
Login_Page: Admin Login
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/0cffdc66-8ca0-4996-986a-7925fa954a82" />
Dashboard_Page(Admin)
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/12149a94-fc76-4fce-8b4a-a03f74bafa5d" />

