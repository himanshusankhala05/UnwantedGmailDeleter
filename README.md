# 🤖 Gmail Extra Mails Deletion Automation

## 📋 Overview
This repository contains an enterprise-grade automation solution built using the **UiPath Robotic Enterprise Framework (REFramework)**. The project is designed to connect to a target Gmail account, identify specified "extra" or bloat emails (based on configured rules, senders, or keywords), and securely delete them to maintain a clean mailbox.

Built on top of UiPath's standard *Transactional Business Process* template, it utilizes a robust **State Machine** layout to ensure high-level logging, advanced exception handling, and seamless error recovery.

---

## ⚙️ How It Works (REFramework States)

### 1. Initialization (INITIALIZE PROCESS)
* `Framework/InitAllSettings.xaml`: Loads operational data, filtration keywords, and Gmail folder names from the `Config.xlsx` file and UiPath Orchestrator assets.
* `Framework/GetAppCredential.xaml`: Securely retrieves Gmail API tokens or account credentials from Orchestrator Assets or the Windows Credential Manager.
* `Framework/InitAllApplications.xaml`: Opens the required browser/interface or establishes a secure IMAP/API connection to Gmail.

### 2. Data Retrieval (GET TRANSACTION DATA)
* `Framework/GetTransactionData.xaml`: Fetches the target email list. By default, it retrieves unread/specific emails from a configured Gmail folder or an Orchestrator Queue containing email IDs to process.

### 3. Execution (PROCESS TRANSACTION)
* `Process.xaml`: Inspects each individual email against your deletion criteria (e.g., newsletters, promotions, age of email). If it matches, the workflow invokes the deletion sequence.
* `Framework/SetTransactionStatus.xaml`: Updates the status of the processed email. Marks it as **Success** (Deleted/Archived), **Business Rule Exception** (e.g., email did not match criteria, skipped safely), or **System Exception** (e.g., connection drop).

### 4. Wrap Up (END PROCESS)
* `Framework/CloseAllApplications.xaml`: Safely disconnects from the Gmail server, logs out of any open web sessions, and closes the browser cleanly.

> 💡 **Note:** In the event of a *System Exception*, the framework automatically takes a desktop
