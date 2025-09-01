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

## 🗄️ Step 1 — Open MariaDB shell as local root

```bash
sudo mysql -u root -p
```

---
## 🔑 Option-1 — Give Full Privileges to root user
### 1) → 👤🔑⭐ Create user & Give full Privileges:
```sql
select user, host from mysql.user;
```
```
CREATE USER 'root'@'%' IDENTIFIED BY 'admin';
```
```
select user, host from mysql.user;
```
```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
```
```
FLUSH PRIVILEGES;
```
```
EXIT;
```

### 2) Restart MariaDB → 🔄 🐬
```bash
sudo systemctl restart mariadb
```
### 3) Allow firewall port → 🔥🔓 or 🔥📡
```
sudo ufw allow 3306/tcp
```
```
sudo ufw reload
```


---
✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦    
---

## ✅ Option-2 (Create a Limited Access Remote User)
## 🔒 Safer Alternative (Recommended)

Instead of exposing the root account remotely, create a dedicated user with limited access to only the databases that user needs.

### Create a Limited Access Remote User
### Step 1 → 🖥️🔑 Login to MySQL
```sql
sudo mysql -u root -p
```
### Step 2 → 📋👤💾 To See List of User & Database Name:
```
select user, host from mysql.user;
```
### Step 3 → 👤➕🔑 Create User & Password:
```
CREATE USER 'erpnext'@'%' IDENTIFIED BY 'StrongPa$$w0rd!';
```
### Step 4 → 🎟️🔒 Grand Limited Privileges:
```
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX 
ON _916e2dbd66f00f1b.* 
TO 'erpnext'@'%';
```
- Replace `_916e2dbd66f00f1b` and `StrongPa$$w0rd!` & use a strong password.
- See Database Name in mysql:
### Step 5 → 📚💾 See List of Databases & Name:
```
SHOW DATABASES;
```
### Step 6 → 🔄🔐 Flush Privileges:
```
FLUSH PRIVILEGES;
```
### Step 7 → 🚪↩️ Exit from mysql:
```
EXIT;
```

### Step 8 → 🔄 🐬 Restart MariaDB 
```bash
sudo systemctl restart mariadb
```
### Step 9 → 🔥🔓 or 🔥📡 Allow firewall port 
```
sudo ufw allow 3306/tcp
```
```
sudo ufw reload
```

---

## 🛠️ Configure MariaDB to listen on all interfaces

Open the server configuration and change bind-address:

```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```
##  (bind-address = 127.0.0.1)  --->  change to: (bind-address = 0.0.0.0)
```
sudo systemctl restart mariadb
```

If your distribution uses `/etc/mysql/my.cnf` or another conf file, update that instead.

---
✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦   
---

## 🐬 <img width="28" height="28" alt="MySQL" src="https://www.mysql.com/common/logos/logo-mysql-170x115.png" /> Install MySQL database Connector:   
Download Any Latest Driver & Install :
https://dev.mysql.com/downloads/connector/odbc/    

<img width="548" height="420" alt="image" src="https://github.com/user-attachments/assets/6650fcfb-e8a8-4aed-a64f-2ed80fdb4d75" />

---
✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦  
---

## <img width="35" height="35" alt="Power BI" src="https://github.com/user-attachments/assets/63f8afd1-86e5-491f-a3f5-d40d53d26e3a" /> Connect Power BI:

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
✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦
---

## 🔍 Troubleshooting

- **Connection refused:** Check `bind-address` and that MariaDB is listening on `0.0.0.0`.
- **Firewall blocked:** Ensure `ufw` allows `3306/tcp` and any cloud provider security groups permit it.
- **Authentication errors:** Confirm the username, host wildcard (`%`), and password are correct.
- **Multiple root rows:** You can have `root@localhost` and `root@%` simultaneously. Use carefully.

### Helpful commands:

```bash
# see listening ports
sudo ss -tulpn | grep mysql

# show mysql users
sudo mysql -u root -p -e "SELECT User, Host FROM mysql.user;"
```

---

## ⚠️ Security Warnings (Please Read)

- Exposing port 3306 to the public internet is **dangerous**. Prefer VPN (WireGuard/OpenVPN) or SSH tunneling.
- **Never** use simple passwords like `admin` in production. Use a password manager.
- Consider enabling `require_secure_transport = ON` (TLS) and use client certificates for stricter security.

---

## ✅ Rollback — Revoke remote privileges

If you want to remove remote root access:

```sql
-- run inside mysql
DROP USER 'root'@'%';
FLUSH PRIVILEGES;
EXIT;
```

And close firewall port:

```bash
sudo ufw delete allow 3306/tcp
sudo ufw reload
```

---

## ❓ FAQ

**Q: Is `bind-address = 0.0.0.0` safe?**  
A: It makes MariaDB accept connections from any IP — use it only together with firewall rules and restricted DB users.

**Q: How can I secure connections?**  
A: Use SSL/TLS for MariaDB, restrict hosts in user definitions, or use a VPN/SSH tunnel.

---

## 🧾 License

MIT — feel free to copy, adapt, and use.

---

If you'd like, I can:

- convert this to a single-file README.md for your repo (already done here),
- add SVG badges for your project, or
- generate a small `setup.sh` that runs selected steps (I'll include safety prompts).

**Which would you prefer next? 🙂**
