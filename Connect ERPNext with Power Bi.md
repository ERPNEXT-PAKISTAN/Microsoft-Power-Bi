<p align="center">
   <img width="195" height="70" alt="Power BI" src="https://github.com/user-attachments/assets/b6b12445-4a2b-4f34-92c4-7819e5c491cc" />
   <img width="200" height="200" alt="Remote Access" src="https://github.com/user-attachments/assets/ccdd6e3e-27ce-4adf-83ee-703873fce743" />
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

### 3) Restart MariaDB
```bash
sudo systemctl restart mariadb
```
### 3) Allow firewall port
```
sudo ufw allow 3306/tcp
```
```
sudo ufw reload
```


---

## ✅ Option-2 (Create a Limited Access Remote User)
## 🔒 Safer Alternative (Recommended)

Instead of exposing the root account remotely, create a dedicated user with limited access to only the databases that user needs.

### Create a limited remote user

```sql
sudo mysql -u root -p
```
- To See List of User & Database Name:
```
select user, host from mysql.user;
```
```
CREATE USER 'erpnext'@'%' IDENTIFIED BY 'StrongPa$$w0rd!';
```
```
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX 
ON _916e2dbd66f00f1b.* 
TO 'erpnext'@'%';
```
- Replace `_916e2dbd66f00f1b` and `StrongPa$$w0rd!` & use a strong password.
- See Database Name:
```
SELECT DATABASE();
```
```
FLUSH PRIVILEGES;
```
```
EXIT;
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


## 🐬 <img width="28" height="28" alt="MySQL" src="https://www.mysql.com/common/logos/logo-mysql-170x115.png" /> Install MySQL database Connector:   
Download Any Latest Driver & Install :
https://dev.mysql.com/downloads/connector/odbc/    

<img width="548" height="420" alt="image" src="https://github.com/user-attachments/assets/7a25eea8-24f0-4994-84b1-a0a013896ab5" />

---

## <img width="35" height="35" alt="Power BI" src="https://github.com/user-attachments/assets/f206b895-2362-4599-b67e-7563d31fe77d" /> Connect Power BI:

<p align="center">
  <img width="48" height="48" alt="Power BI" src="https://github.com/user-attachments/assets/f206b895-2362-4599-b67e-7563d31fe77d" />
  <strong>
    <span style="font-size:2em;">Connect with Microsoft Power BI:</span>
  </strong>
  <img width="48" height="48" alt="Power BI" src="https://github.com/user-attachments/assets/2a6a9585-b299-4e68-a3fc-dfdb12af8231" />
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
<img width="715" height="291" alt="image" src="https://github.com/user-attachments/assets/96a7d63f-1bc8-431a-bf7f-8edcc5573e4b" />
<img width="711" height="394" alt="image" src="https://github.com/user-attachments/assets/11c70708-a38d-4141-a97a-92bb984dfd66" />



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
