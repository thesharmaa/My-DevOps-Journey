## What is Shebang?
`A shebang (`#!`) is the first line in a script that tells the Linux kernel which interpreter to use (like Bash or Python) when the file is executed directly. When you run the script, the kernel reads the shebang and automatically launches the specified interpreter to run the script.`|


🚀 Bash Shell Scripting Practice – DevOps Learning Journey

This repository contains beginner-friendly Bash shell scripting tasks focused on Linux automation and DevOps fundamentals.

📚 Tasks Covered

🔹 Task 1: First Shell Script

* Created `hello.sh`
* Added shebang (`#!/bin/bash`)
* Printed `Hello, DevOps!`
* Learned executable permissions using:

```bash
chmod +x hello.sh
./hello.sh
```

💡 Learned:
The shebang line tells Linux which interpreter should execute the script. Without it, the script may still work in some shells but becomes less portable and reliable.

---

🔹 Task 2: Variables
Created `variables.sh` using:

* Variables for NAME and ROLE
* Dynamic output using `echo`

💡 Learned:

* Double quotes `" "` allow variable expansion
* Single quotes `' '` treat text literally

---

🔹 Task 3: User Input
Created `greet.sh` using:

* `read` command for user input
* Personalized output messages

---

🔹 Task 4: If-Else Conditions
Created:

* `check_number.sh`
* `file_check.sh`

Concepts practiced:

* Conditional statements
* Numeric comparisons
* File existence check using `-f`

---

🔹 Task 5: Service Status Automation
Created `server_check.sh`

Features:

* Stores service name in variable
* Takes user confirmation
* Checks service status using `systemctl`
* Displays whether service is active or skipped

---

🛠 Skills Practiced

* Bash scripting
* Linux commands
* Variables
* User input handling
* Conditional logic
* File handling
* Service monitoring
* Basic automation

📈 Next Steps

* Loops in Bash
* Functions
* Cron jobs
* Log monitoring
* AWS automation scripts
* DevOps project automation

#bash #linux #shellscripting #devops #automation

