# AWS IAM Users and Least Privilege Lab
# Overview  
* This project demonstrates the implementation of AWS Identity and Access Management (IAM) best practices, focusing on **Least Privilege**, **Role-Based Access Control (RBAC)**, and **Separation of Duties**. Three distinct IAM groups and users were configured to model production access boundaries.
# Security Concepts Applied
* **Least Privilege:** Users receive only the permissions required for their specific function.

* **Explicit Deny Overrides Allow:** Customer-managed deny policy takes precedence over attached broad execution policies.

* **Separation of Duties:** Administrative, development, and auditing duties are restricted to separate accounts.
  # IAM Architecture & Access Matrix
**AWS Account**

* 📁 Group: Lab-Administrators

 * 📜 Attached Policy: AdministartorAcess

 * 👤User: lab-admin

##                                ##

* 📁 Group: Lab-Developers

* 📜 Attached Policy: AmazonEC2FullAccess

* 📜 Attached Policy: Deny-EC2-Termination (Custom JSON)

* 👤 User: lab-developer

##                                 ##

* 📁 Group: Lab-Auditors
   
* 📜 Attached Policy: AmazonEC2ReadOnlyAccess
    
 * 👤 User: lab-auditor

# Hands-On Verification & Screenshots
### 1. Auditor Account Verification
* **Test:** Sign in as `lab-auditor` and view resources vs. attempting modification.
* **Result:** Read operations succeeded resource launch/modification was blocked.
* ![Auditor Access Denied](<img width="946" height="515" alt="Screenshot 2026-08-24 184037" src="https://github.com/user-attachments/assets/fbcefea7-856c-4da5-8010-a59d5228217f" />)

*Figure 1: AWS Console/CLI throwing an access authorization failure when `lab-auditor` attempts restricted state changes.*





    
