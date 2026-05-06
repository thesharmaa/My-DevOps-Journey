# 🚀 Linux User & Group Management Challenge

## 🎯 Objective
Practice real-world Linux user & group management:
- Create users & set passwords
- Create groups & assign users
- Manage shared directories with permissions
- Simulate a team workspace

---

## 👥 Users & Groups Created

### Users:
- tokyo
- berlin
- professor
- nairobi

### Groups:
- developers
- admins
- project-team

---

## 🔗 Group Assignments

| User      | Groups                  |
|-----------|------------------------|
| tokyo     | developers, project-team |
| berlin    | developers, admins     |
| professor | admins                 |
| nairobi   | project-team           |

👉 Verify:
```bash
groups username
````

---

## 📂 Directories Created

| Directory           | Group        | Permissions |
| ------------------- | ------------ | ----------- |
| /opt/dev-project    | developers   | 775         |
| /opt/team-workspace | project-team | 775         |

👉 Verify:

```bash
ls -ld /opt/dev-project
ls -ld /opt/team-workspace
```

---

## ⚙️ Commands Used

### 🔹 User Management

```bash
sudo useradd -m tokyo
sudo passwd tokyo

sudo useradd -m berlin
sudo passwd berlin

sudo useradd -m professor
sudo passwd professor

sudo useradd -m nairobi
sudo passwd nairobi
```

---

### 🔹 Group Management

```bash
sudo groupadd developers
sudo groupadd admins
sudo groupadd project-team
```

---

### 🔹 Assign Users to Groups

```bash
sudo usermod -aG developers tokyo

sudo usermod -aG developers berlin
sudo usermod -aG admins berlin

sudo usermod -aG admins professor

sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
```

---

### 🔹 Directory Setup

```bash
sudo mkdir -p /opt/dev-project
sudo chgrp developers /opt/dev-project
sudo chmod 775 /opt/dev-project

sudo mkdir -p /opt/team-workspace
sudo chgrp project-team /opt/team-workspace
sudo chmod 775 /opt/team-workspace
```

---

### 🔹 Testing Access

```bash
sudo -u tokyo touch /opt/dev-project/test.txt
sudo -u berlin touch /opt/dev-project/test2.txt

sudo -u nairobi touch /opt/team-workspace/file.txt
```

---

## ⚠️ Common Mistakes (Important 🔥)

❌ Using wrong command for adding users to groups
👉 Always use:

```bash
usermod -aG group user
```

❌ Forgetting `-a` flag
👉 Without `-a`, existing groups get overwritten

❌ Setting permissions but forgetting group ownership
👉 Fix:

```bash
chgrp group directory
```

❌ Assuming `chmod 775` alone is enough
👉 Access = **Ownership + Permissions**

---

## 💡 Key Learnings

1. **Users = identities**, Groups = **roles**
2. **Groups simplify permission management at scale**
3. Real access control depends on:

   ```
   User + Group + Ownership + Permissions
   ```

---

## 🧪 Troubleshooting

### Permission denied?

```bash
sudo command
```

### User can't access directory?

Check group:

```bash
groups username
```

Check permissions:

```bash
ls -ld /path
```

---

## 🌍 Real-World DevOps Use

* Managing team access to servers
* Controlling deployment permissions
* Shared project directories in production
* Avoiding accidental access issues

---

## 🧠 Quick Revision (1-Min Recap)

* Create user → `useradd -m`
* Set password → `passwd`
* Create group → `groupadd`
* Add user → `usermod -aG`
* Set group → `chgrp`
* Set permission → `chmod 775`
* Test → `sudo -u user`

👉 **Golden Rule:**

> If access fails → check *Group + Ownership + Permissions*


