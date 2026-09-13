# Linux User & Group Management System

![Linux User & Group Management Verification](./usermanagementproject.jpg)

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

### Step 1: Create Groups
Created two primary user groups for departmental segregation:
```bash
sudo groupadd cloud-engineers
sudo groupadd devops
