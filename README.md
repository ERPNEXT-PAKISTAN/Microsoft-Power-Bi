<p align="center">
  <img width="115" height="115" alt="Remote Access" src="https://github.com/user-attachments/assets/657bb777-d9e1-43cb-aab5-2c8b39029c0c" style="vertical-align:bottom;" />
  <img width="200" height="200" alt="Arrow" src="https://github.com/user-attachments/assets/4c24c8fc-e16a-4a7c-bf9a-c0f0a36a4f58" style="vertical-align:bottom;" />
  <img width="115" height="115" alt="EM" src="https://github.com/user-attachments/assets/2d671067-7c17-481a-835a-e1d981c08ce1" style="vertical-align:bottom;" />
</p>

# 🚀 Enable Remote Access To Connect Microsoft Power BI

Easily and securely enable remote access for MariaDB, so you can connect your data to Power BI.  

---

## ⚡️ Quick Options

| Option | Description | Risk Level |
|--------|-------------|------------|
| ⚠️ Option-1 | **Give Full Privileges to root user** | **High risk** |
| ✅ Option-2 | **Create a limited access remote user (Recommended)** | **Safe** |

> **Important:** Giving `root@'%'` full privileges is risky. See the **Safer Alternative** section.

---

### 🗄️ Step 1 — Open MariaDB shell as local root

### 🔑 Option-1 — Give Full Privileges to root user
### ✅ Option-2 (Create a Limited Access Remote User)
### 🔒 Safer Alternative (Recommended)
### Create a Limited Access Remote User
### Step 1 — Login to MySQL
### 🛠️ Configure MariaDB to listen on all interfaces
### 🐬 <img width="28" height="28" alt="MySQL" src="https://www.mysql.com/common/logos/logo-mysql-170x115.png" /> Install MySQL database Connector:   

<img width="548" height="420" alt="image" src="https://github.com/user-attachments/assets/6650fcfb-e8a8-4aed-a64f-2ed80fdb4d75" />
---
### <img width="35" height="35" alt="Power BI" src="https://github.com/user-attachments/assets/63f8afd1-86e5-491f-a3f5-d40d53d26e3a" /> Connect Power BI:

<p align="center">
   <img width="48" height="48" alt="Power" src="https://github.com/user-attachments/assets/3adf0802-030b-4f5b-a6fa-4a5a058ac619" />
  <strong>
    <span style="font-size:2em;">Connect Microsoft Power Bi with ERPNext :</span>
  </strong>
    <img width="48" height="48" alt="Power" src="https://github.com/user-attachments/assets/3adf0802-030b-4f5b-a6fa-4a5a058ac619" />
</p>

- **IP Address:** `192.168.1.10`
- **Database Name:** `_c12d12dfd54f5dd5`
- **User Name:** `root`
- **Password:** `abc123`

---
### 🔍 Check ERPNext Database Name:
Open ERPNext --> System Console ---> Select Type: SQL

```bash
SELECT DATABASE();
```
---
<img width="718" height="285" alt="Power Conn" src="https://github.com/user-attachments/assets/ee6863cf-f579-47ff-877f-b4c0caaf9223" />
<img width="708" height="387" alt="Power Connt" src="https://github.com/user-attachments/assets/531a0dcb-e70f-4782-bbc7-abcb1fb65468" />

---

## 🔍 Troubleshooting
### Helpful commands:
## ⚠️ Security Warnings (Please Read)
## ✅ Rollback — Revoke remote privileges
