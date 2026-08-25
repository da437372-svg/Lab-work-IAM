# AWS IAM Users and Least Privilege Lab
# Overview  
* This project demonstrates the implementation of AWS Identity and Access Management (IAM) best practices, focusing on **Least Privilege**, **Role-Based Access Control (RBAC)**, and **Separation of Duties**. Three distinct IAM groups and users were configured to model production access boundaries.
# Security Concepts Applied
* **Least Privilege:** Users receive only the permissions required for their specific function.
  
* **Separation of Duties:** Administrative, development, and auditing duties are restricted to separate accounts.

* **Explicit Deny Overrides Allow:** Customer-managed deny policy takes precedence over attached broad execution policies.




### 1. Least Privilege
The following matrix shows the types of users and their roles.
<img width="603" height="103" alt="Screenshot 2026-08-24 203931" src="https://github.com/user-attachments/assets/c0d23969-aa00-49b4-bf19-ac54d20f3455" />


##                      ##



  The access matrix shows how the least privilege was granted to each user.

<img width="612" height="132" alt="Screenshot 2026-08-24 202506" src="https://github.com/user-attachments/assets/603cff74-3fd2-4748-b36c-909961870b10" />

# Hands-On Verification & Screenshots

### 2. Separation of Duties (auditor cannot Launch EC2 instance)


* **Test:** Sign in as `lab-auditor` and try to launch an EC2 instance.
* **Result:** EC2 instance creation will be denied.
* [Auditor Access Denied]
 <img width="946" height="515" alt="Screenshot 2026-08-24 184037" src="https://github.com/user-attachments/assets/32347a1e-c945-47f9-a81f-b0fba0e163e3" />


*Figure 1: The auditor cannot launch an EC2 instance, because of AmazonEC2ReadOnlyAccess policy*


### 3. Developer Account Verification (Explicit Deny Test)
* **Test:** Launch instance `iam-developer-test`, stop/start it, and attempt instance termination.
* **Result:** EC2 creation, start, and stop succeeded. Instance termination failed due to explicit deny policy

[Deny EC2 Termination] <img width="1225" height="296" alt="Screenshot 2026-08-24 194701" src="https://github.com/user-attachments/assets/c44e1cb9-5587-4e46-835a-55e9424fdf3e" />

*Figure 2: Console error showing `You are not authorized to perform this operation` when `lab-developer` executes instance termination*

---

### 4. Terminate the test instance (Admin can terminate EC2)
* **Test:** Sign in as `lab-admin` and terminate `iam-developer-test`.
* **Result:** Successful termination Administrator does not inherit the developer's explicit deny rule.

[Admin Termination Success] <img width="1230" height="316" alt="Screenshot 2026-08-24 194826" src="https://github.com/user-attachments/assets/524234dc-c0d2-4b71-8a36-e812733231a5" />

*Figure 3: `lab-admin` successfully terminating the test instance.*

---
## Environment Cleanup
To maintain cloud hygiene and prevent unnecessary costs, all lab resources were removed in sequence:
1. Terminated active EC2 instances.
2. Removed IAM users (`lab-admin`, `lab-developer`, `lab-auditor`).
3. Removed IAM groups (`Lab-Administrators`, `Lab-Developers`, `Lab-Auditors`).
4. Deleted custom policy `Deny-EC2-Termination`.






    
