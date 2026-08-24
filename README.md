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
* ![Auditor Access Denied] ./<img width="946" height="515" alt="Screenshot 2026-08-24 184037" src="https://github.com/user-attachments/assets/32347a1e-c945-47f9-a81f-b0fba0e163e3" />


*Figure 1: AWS Console/CLI throwing an access authorization failure when `lab-auditor` attempts restricted state changes.*

### 2. Developer Account Verification (Explicit Deny Test)
* **Test:** Launch instance `iam-developer-test`, stop/start it, and attempt instance termination.
* **Result:** EC2 creation, start, and stop succeeded. Instance termination failed due to explicit deny policy

![Developer Termination Denied](./<img width="1225" height="296" alt="Screenshot 2026-08-24 194701" src="https://github.com/user-attachments/assets/c44e1cb9-5587-4e46-835a-55e9424fdf3e" />
)
*Figure 2: Console error showing `You are not authorized to perform this operation` when `lab-developer` executes instance termination*

---

### 3. Administrator Account Verification & Cleanup
* **Test:** Sign in as `lab-admin` and terminate `iam-developer-test`.
* **Result:** Successful termination Administrator does not inherit the developer's explicit deny rule.

![Admin Termination Success](./<img width="1230" height="316" alt="Screenshot 2026-08-24 194826" src="https://github.com/user-attachments/assets/524234dc-c0d2-4b71-8a36-e812733231a5" />
)
*Figure 3: `lab-admin` successfully terminating the test instance.*

---
## Environment Cleanup
To maintain cloud hygiene and prevent unnecessary costs, all lab resources were removed in sequence:
1. Terminated active EC2 instances.
2. Removed IAM users (`lab-admin`, `lab-developer`, `lab-auditor`).
3. Removed IAM groups (`Lab-Administrators`, `Lab-Developers`, `Lab-Auditors`).
4. Deleted custom policy `Deny-EC2-Termination`.






    
