
<img width="1312" height="1199" alt="project" src="https://github.com/user-attachments/assets/addc79f3-cfd8-43f4-849e-fc6aa0f293a3" />

# Linux User & Group Management System

![Linux User & Group Management Verification](project.jpg)

## 📌 Project Overview
This project demonstrates **Linux User & Group Management**, Access Control, and File Permissions configured on a Linux server (Kali Linux) based on real-world enterprise requirements for Cloud Engineering and DevOps departments.

---

## 🎯 Project Scenario
A cloud company hired 3 new employees and required structured role-based access control (RBAC) on the Linux server following the **Principle of Least Privilege**.

### Team Members & Roles
- 👤 **Ali** — Cloud Engineer
- 👤 **Ahmed** — DevOps Engineer
- 👤 **Sara** — Cloud Intern

---

## ⚙️ Requirements & Access Policy Matrix

| User | Role | Assigned Groups | Access to `/cloud-project` |
| :--- | :--- | :--- | :---: |
| **Ali** | Cloud Engineer | `cloud-engineers` | ✅ Allowed |
| **Sara** | Cloud Intern | `cloud-engineers`, `devops` | ✅ Allowed |
| **Ahmed** | DevOps Engineer | `devops` | ❌ Denied |

---

## 🛠️ Implementation Steps

<img width="953" height="521" alt="scrshort" src="https://github.com/user-attachments/assets/0fe0d8cb-7161-4580-a200-e8539c154654" />

### Step 1: Create Groups
Created two primary user groups for departmental segregation:


sudo groupadd cloud-engineers
sudo groupadd devops

Step 2: Create User Accounts
Created 3 user accounts with their respective home directories:

Bash
sudo useradd -m ali
sudo useradd -m ahmed
sudo useradd -m sara
Step 3: Assign Users to Groups
Assigned users to their corresponding role-based groups:

Bash
sudo usermod -aG cloud-engineers ali
sudo usermod -aG devops ahmed
sudo usermod -aG cloud-engineers,devops sara
Step 4: Configure Shared Resource Directory
Created a shared project directory /cloud-project restricted strictly to members of the cloud-engineers group using 770 permissions (rwxrwx---):

Bash
sudo mkdir /cloud-project
sudo chgrp cloud-engineers /cloud-project
sudo chmod 770 /cloud-project
sudo touch /cloud-project/cloud-project.txt
🧪 Verification & Results
1. User & Group Membership Inspection
Inspected system database and group memberships using getent and id commands:

Bash
getent passwd ali ahmed sara
id ali
id sara
id ahmed
2. Access Control Testing (Least Privilege Verification)
Switching shell sessions to test access rights against /cloud-project:

Bash
# Ali (Cloud Engineer) - Access Granted
sudo -iu ali
whoami  # ali
ls /cloud-project  # Success: cloud-project.txt visible

# Sara (Cloud Intern) - Access Granted
sudo -iu sara
whoami  # sara
ls /cloud-project  # Success: cloud-project.txt visible

# Ahmed (DevOps Engineer) - Access Denied
sudo -iu ahmed
whoami  # ahmed
ls /cloud-project  # Result: ls: cannot open directory '/cloud-project': Permission denied
Terminal Output Proof
🧹 User Offboarding (Cleanup)
Safely removed Ahmed's account and home directory while retaining the devops group for future hiring:

Bash
sudo userdel -r ahmed
id ahmed             # Output: no such user
getent group devops  # Output: devops group retained
💡 Key Learnings
User & Group Administration: Creating, modifying, and managing system users and security groups.

Linux File Permissions: Implementing chmod, chgrp, and numerical permission masks (770).

Least Privilege Principle: Restricting access so team members only access files essential to their role.

Enterprise Offboarding: Proper user deletion while maintaining group structure integrity.


<img width="953" height="521" alt="scrshort" src="https://github.com/user-attachments/assets/0fe0d8cb-7161-4580-a200-e8539c154654" />
```bash
