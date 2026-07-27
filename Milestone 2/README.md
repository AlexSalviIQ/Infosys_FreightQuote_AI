# Maritime Logistics Intelligence Platform — Milestone 2

## Overview & Progression from Milestone 1
Milestone 2 transitions the platform from a foundational data processing baseline (Milestone 1) into a secure, fully interactive, multi-agent intelligence ecosystem. While Milestone 1 focused on standalone calculations and basic script logic, Milestone 2 builds a unified **Streamlit dashboard orchestration layer** driven by autonomous agents, secured by localized database authentication, and augmented by a Generative AI executive advisory copilot.

---

## Key Features Built
*   **Security Gateway Lockout:** Secure User Authentication (Login, Register, Password Recovery) utilizing Gmail OTP verification, role-based routing (`User` vs `Admin`), and progressive account lockout mechanics enforced via an SQLite backend.
*   **Domain Intelligence Engine:** Three autonomous tabular reasoning modules providing real-time operational forecasting:
    *   *Agent 1 (Dynamic Freight Pricing):* Predicts dynamic shipping rates based on container types, fuel indices, and seasonal demand variations.
    *   *Agent 2 (Route Delay Classifier):* Classifies potential shipping delays based on historical port congestion, weather conditions, and transit vectors.
    *   *Agent 3 (Carrier Compliance Sentinel):* Evaluates maritime carrier risk profiles, insurance updates, and regulatory compliance flags.
*   **Generative Executive Advisory:** A centralized LLM Copilot that swallows the structured mathematical outputs of the three autonomous agents and synthesizes them into actionable shipping strategy briefs and structured JSON logistics audits.
*   **System Administration Controls:** An isolated administrative control panel allowing user role management, system telemetry logs, and manual security overrides.

---

## Tech Stack Used
*   **Core UI & Orchestration:** Streamlit (v1.35.0+)
*   **Database & Storage:** SQLite3 (State retention & user credentials)
*   **AI Engine & Tooling:** Hugging Face Inference API (`mistralai/Mixtral-8x7B-Instruct-v0.1`), LangChain / Custom Agent Prompts
*   **Security & Encryption:** PyJWT, Passlib (SHA-256 password hashing), SMTPLIB (Gmail OTP transport)
*   **Data Processing:** Pandas, NumPy, Scikit-Learn

---

## System Architecture

The ecosystem operates across a strict 4-Phase pipeline to ensure security, modular execution, and executive synthesis:

| Phase | Module / Component | Responsibility & Workflow |
| :--- | :--- | :--- |
| **Phase 1** | **Security Gateway** | *Authentication & JWT:* Enforces Login, Registration, and Forgot Password (Gmail OTP) before unlocking the UI. Stores hashed credentials and progressive lockout state in SQLite (`users` table). |
| **Phase 2** | **Domain Intelligence** | *3 Autonomous Agents:* Once authenticated, unlocks **Agent 1: Dynamic Pricing**, **Agent 2: Route Delay Classifier**, and **Agent 3: Carrier Compliance Sentinel** tabs. |
| **Phase 3** | **Generative Advisory** | *LLM Copilot & JSON:* Integrates HuggingFace LLM orchestration (`llm_engine_freight.py`) to synthesize the 3 agents' numerical outputs into executive shipping strategies and structured JSON audit actions. |
| **Phase 4** | **System Administration** | *Admin Dashboard:* Dedicated administrative controls (`admin_dash.py`) restricted exclusively to users authenticated with `role = 'Admin'`. |

---

## Localized Indian Port Coverage
The intelligence matrices in Milestone 2 are configured to analyze operational risk, tariffs, and bottlenecks across the major maritime trading nodes of India:

| Port Node | Code | Core Focus Area | Primary Commodities Monitored |
| :--- | :--- | :--- | :--- |
| **Mumbai (JNPT)** | INNSA | Container congestion, seasonal monsoon delays | Electronics, Textiles, Machinery |
| **Mundra** | INMUN | High-throughput dynamic pricing tariff models | Dry Bulk, Chemicals, Automotive |
| **Chennai** | INMAA | Coromandel coast route delay vectors | Industrial Spares, Finished Goods, Iron Ore |
| **Cochin** | INCOK | International transshipment tracking & compliance | Spices, Seafood, Liquid Cargo |

---

## Setup & Configuration Instructions

### 1. Generating API Credentials

#### A. Kaggle API Credentials
1. Log into your account on [Kaggle](https://www.kaggle.com).
2. Click on your profile picture in the top right corner and navigate to **Settings**.
3. Scroll down to the **API** section.
4. Click **Create New Token**. This will automatically download a file named `kaggle.json`.
5. Open `kaggle.json` to extract your `username` and `key`.

#### B. Hugging Face Access Token
1. Log into your account on [Hugging Face](https://huggingface.co).
2. Go to your **Profile Settings** -> **Access Tokens**.
3. Click **New token**.
4. Set the token name (e.g., `maritime-logistics-m2`) and assign it **Read** access.
5. Copy the generated token string (`hf_...`).

---

### 2. Injecting Google Colab Secrets
To protect runtime credentials, do not hardcode your tokens inside the notebook cell layout. Use Colab's native Secret Vault:

1. Open your project notebook in Google Colab.
2. In the left-hand sidebar, click the **Key icon** (Secrets).
3. Add the following key-value pairs exactly as specified:
   * **Name:** `KAGGLE_USERNAME` $\rightarrow$ **Value:** *[Your Kaggle Username]*
   * **Name:** `KAGGLE_KEY` $\rightarrow$ **Value:** *[Your Kaggle API Key API String]*
   * **Name:** `HF_TOKEN` $\rightarrow$ **Value:** *[Your Hugging Face Access Token]*
   * **Name:** `SMTP_PASSWORD` $\rightarrow$ **Value:** *[Your Google App Password for OTP routing]*
4. Toggle the **Notebook Access** switch to **ON** for all injected keys.

---

## How to Run the Notebook & Dashboard

Follow these steps sequentially within the execution environment:

1. **Environment Provisioning:** Run the initial setup cells to install dependencies:
   ```bash
   !pip install streamlit pyjwt passlib requests pandas scikit-learn
Credential Mount: The notebook will automatically ingest the Colab secrets and instantiate the Kaggle environment configuration via:

Python
import os
from google.colab import secrets
os.environ['KAGGLE_USERNAME'] = secrets.get('KAGGLE_USERNAME')
os.environ['KAGGLE_KEY'] = secrets.get('KAGGLE_KEY')
Data Pull: Execute the data collection module to download the maritime tabular datasets directly via the Kaggle CLI.

Bootstrapping the Streamlit Application: Run the cell containing the %%writefile app.py block to write the dashboard architecture script out to disk.

Localtunnel Exposure: Run the execution cell initializing streamlit concurrently alongside localtunnel to generate an external URL:

Bash
!streamlit run app.py & npx localtunnel --port 8501
Click the generated localtunnel link, input the external IP displayed in the terminal output, and log in through the Phase 1 Security Gateway.
