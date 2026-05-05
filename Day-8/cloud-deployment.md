Here’s your **upgraded, advanced GitHub README** with badges, icons, clean structure, and a table of contents 👇

---

# 🚀 First Cloud Deployment with NGINX (AWS EC2)

![AWS](https://img.shields.io/badge/Cloud-AWS-orange?logo=amazonaws\&logoColor=white)
![NGINX](https://img.shields.io/badge/Web%20Server-NGINX-green?logo=nginx\&logoColor=white)
![Linux](https://img.shields.io/badge/OS-Linux-yellow?logo=linux\&logoColor=black)
![DevOps](https://img.shields.io/badge/Domain-DevOps-blue)
![Status](https://img.shields.io/badge/Project-Live-success)

---

## 📌 Overview

Deployed my **first website on a cloud server** using:

* ☁️ Amazon Web Services (EC2 - Ubuntu)
* 🌐 NGINX
* 🔐 SSH (Key-based authentication)

This repo contains:

* Step-by-step setup
* Real debugging scenario (403 error)
* Key DevOps learnings

---

## 📚 Table of Contents

* [🔧 Setup Guide](#-setup-guide)
* [🚨 Debugging Case: 403 Forbidden](#-debugging-case-403-forbidden)
* [🧠 Key Learnings](#-key-learnings)
* [🧪 Debugging Checklist](#-debugging-checklist)
* [🚀 Next Steps](#-next-steps)

---

# 🔧 Setup Guide

## 1️⃣ 🔐 Secure Private Key

```bash
chmod 700 <key-name.pem>
```

👉 Only owner can access the key
⚠️ SSH will fail if permissions are too open

---

## 2️⃣ 🖥️ Connect to Server

```bash
ssh -i <key-name.pem> ubuntu@<ip-address>
```

👉 Secure login into EC2 instance

---

## 3️⃣ 📦 Update Packages

```bash
sudo apt-get update
```

👉 Refresh package list

---

## 4️⃣ ⚙️ Install NGINX

```bash
sudo apt-get install nginx
```

👉 Installs web server

---

## 5️⃣ 👥 Configure Ownership

```bash
sudo chown -R ubuntu:www-data /var/www/html/
```

👉 Ensures:

* You can edit files
* NGINX can serve them

---

## 6️⃣ 🔓 Set Permissions

```bash
sudo chmod 755 /var/www/html
```

👉 Required for directory access (execute bit)

---

## 7️⃣ 📤 Upload Files

```bash
scp -i <key-name.pem> <file> ubuntu@<ip-address>:/var/www/html
```

---

## 8️⃣ 📊 Monitor Logs

```bash
sudo tail -f /var/log/nginx/access.log
```

```bash
sudo tail -f /var/log/nginx/error.log
```

---

## 9️⃣ 📥 Download Logs

```bash
scp -i <key-name.pem> ubuntu@<ip-address>:/var/log/nginx .
```

---

# 🚨 Debugging Case: 403 Forbidden

## ❌ Error

```
403 Forbidden: Permission Denied
```

---

## 🔍 Root Causes

### 1️⃣ 📄 Incorrect File Name

* Expected → `index.html`
* Found → `app.html`

---

### 2️⃣ ⚠️ Wrong Permissions

```bash
chmod 744
```

👉 Problem:

* Missing execute (`x`) permission
* NGINX cannot access directory

➡️ Result: 403 error

---

### 3️⃣ 🌐 Security Group Issue

* Port **80 (HTTP)** was blocked

---

## ✅ Fix Applied

```bash
chmod 755 /var/www/html
```

✔️ Enabled directory access
✔️ Corrected file name
✔️ Opened port 80

---

# 🧠 Key Learnings

* 🔑 Permissions are critical
* 🧑‍💻 NGINX runs as `www-data`
* 📜 Logs help identify real issues
* 🚫 403 errors are usually config-related

---

# 🧪 Debugging Checklist

```
✔️ index.html exists
✔️ chmod 755 applied
✔️ correct ownership
✔️ port 80/443 open
✔️ logs checked
```

Just tell me 👍
