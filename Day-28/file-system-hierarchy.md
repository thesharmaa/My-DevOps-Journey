# Linux Filesystem

### ⭐ What is Linux filesystem hierarchy?
The Linux Filesystem Hierarchy (FHS) is a standard way of organizing files & directories in Linux. It defines where different types of files should be stored, such as configuration files, user data, logs, applications, & system files.

Everything in Linux starts from the root directory (`/`).

### ⭐ Why is FHS important?
It provides a standard structure, making it easier for users, administrators & applications to find files across different Linux locations.

### ⭐ Why does Linux have a single root (`/`)?
Linux organizes everything under one top-level directory called the root directory (`/`). Unlike Windows, which uses drives like `C:` & `D:`, Linux attaches all storage devices to this single directory tree.

---

### ⭐ Explain the directory structure of Linux?
Linux organizes files into directories based on their purpose:

| Directory | Purpose |
|---|---|
| `/etc` | Configuration files |
| `/home` | User files |
| `/var` | Logs & changing data |
| `/usr` | Installed software |
| `/boot` | Boot files |
| `/dev` | Device files |
| `/proc` | Process & kernel info |

### ⭐⭐ Is `/` the same as `/root`?
→ No
- `/` → Top-level directory (parent of all directories)
- `/root` → Home directory of the root user

### ⭐ What is `/bin`?
It contains essential user commands like `ls`, `cp`, `mv`, `cat`, etc.

### ⭐ `/bin` vs `/usr/bin`
- `/bin` contains essential commands required (for boot/basic operation)
- `/usr/bin` contains most user applications

### ⭐ What is `/etc` used for?
It stores system configuration files.
Ex: `passwd`, `hosts`, `ssh config`

---

### ⭐ What is stored in `/home`?
It contains personal files for all users.

### ⭐ `/root`?
Home directory of the root user.

### ⭐ `/var`?
It stores changing data like logs, mail, cache & spool.

### ⭐ Where are log files stored?
`/var/log`

### ⭐ What is `/tmp`?
It stores temporary files. These files may be deleted after reboot.

---

