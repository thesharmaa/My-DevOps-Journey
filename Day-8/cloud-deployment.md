🚀 First Cloud Deployment with NGINX (AWS EC2)

Deployed my first website on a cloud server and gained hands-on experience with Linux, SSH, permissions, NGINX, and debugging.

This is a step-by-step guide + real debugging case for future reference.

📌 Overview
Cloud Provider: Amazon Web Services (EC2 - Ubuntu)
Web Server: NGINX
Access Method: SSH (key-based authentication)
🔧 Setup Guide
1️⃣ Secure Private Key (IMPORTANT 🔐)
chmod 700 <key-name.pem>

👉 Restricts access:

Only owner can read/write/execute
No access for group/others

💡 SSH will fail if key permissions are too open.

2️⃣ Connect to Server
ssh -i <key-name.pem> ubuntu@<ip-address>

👉 Secure remote login into EC2 instance

3️⃣ Update Packages
sudo apt-get update

👉 Updates system package list

4️⃣ Install NGINX
sudo apt-get install nginx

👉 Installs and starts web server

5️⃣ Configure Ownership
sudo chown -R ubuntu:www-data /var/www/html/

👉 Ensures:

You can edit files
NGINX (www-data) can serve files
6️⃣ Set Correct Permissions
sudo chmod 755 /var/www/html

👉 Permissions:

Owner → full access
Group & Others → read + execute

💡 Execute (x) is required for directory access

7️⃣ Upload Website Files
scp -i <key-name.pem> <file> ubuntu@<ip-address>:/var/www/html

👉 Transfers files to server

8️⃣ Monitor Logs
sudo tail -f /var/log/nginx/access.log

👉 View incoming traffic

sudo tail -f /var/log/nginx/error.log

👉 Debug errors

9️⃣ Download Logs (Optional)
scp -i <key-name.pem> ubuntu@<ip-address>:/var/log/nginx .

👉 Analyze logs locally

🚨 Debugging Case: 403 Forbidden
❌ Error
403 Forbidden: Permission Denied
🔍 Root Causes
1️⃣ Incorrect File Name
NGINX expects: index.html
Found: app.html
2️⃣ Wrong Permissions (Critical ⚠️)
chmod 744

👉 Problem:

No execute (x) permission on directory
NGINX cannot access files

➡️ Result: 403 Forbidden

3️⃣ AWS Security Group Issue
Port 80 (HTTP) was closed

➡️ Website not accessible

✅ Fix Summary
chmod 755 /var/www/html

✔️ Added execute permission
✔️ Renamed file → index.html
✔️ Opened port 80 in EC2 security group

🧠 Key Learnings
🔑 Permissions Matter
Read ≠ enough
Execute (x) required for directories
🧑‍💻 NGINX Runs as Separate User
Usually www-data
Needs access to your files
📜 Logs Are Your Best Friend
access.log → traffic
error.log → issues
🚫 403 ≠ Code Issue

Usually caused by:

Permissions
File name
Server config
🧪 Debugging Checklist
✔️ index.html exists
✔️ chmod 755 on directories
✔️ Correct ownership (www-data)
✔️ Port 80/443 open
✔️ Check logs
🚀 Final Thoughts

Small setup, big learning.

This project gave real exposure to:

Linux fundamentals
Web server setup
Real-world debugging
