## 🔹 Process in Linux

* A process in Linux is a running instance of a program managed by the kernel.

* Processes are typically created using the fork() system call, which creates a child process as a copy of the parent.

* The child can then use exec() to replace its memory space with a new program.

* The kernel manages processes through scheduling, allocating CPU time, and tracking them using a Process Control Block (PCB), which stores information like process ID, state, registers, and memory details.

* Memory is handled using virtual memory, giving each process its own isolated address space.

* Each process goes through states such as running, ready, waiting (blocked), and terminated.

---

## 🔹 Kernel

* The kernel is the core component of an operating system that acts as a bridge between user applications and the hardware.

* It manages system resources such as CPU, memory, and I/O devices, and provides services to programs through system calls.

* It sits between hardware and software, ensuring that applications don’t access hardware directly but request resources in a controlled way.

* The kernel is responsible for process management, memory management using virtual memory, device management through drivers, and file system management.

* It ensures efficient and secure execution of programs.

---

## 🔹 User Space

* User space is the part of the system where user applications run with restricted privileges.
* Applications in user space cannot directly access hardware; instead, they interact with the kernel using system calls.
* This separation between user space and kernel space ensures security, stability, and prevents applications from interfering with each other or the system.

---

## 🔹 Init

* Init is the first user-space process started by the kernel during the boot process, and it always has PID 1

* It acts as the parent of all other processes and is responsible for initializing the system by starting essential services like networking and SSH.

* After the kernel loads, it directly starts init, which then brings the system to a usable state by launching and managing services.

* Traditional init systems like System V init start services sequentially, which can be slower and harder to manage.

* Modern Linux systems use systemd, which improves startup speed through parallel execution and better dependency handling

---

## 🔹 systemd

* systemd is the modern init system used in most Linux distributions, and it runs as the first user-space process with PID 1.

* It is responsible for initializing the system, starting and managing services, and bringing the system to a usable state.

* Compared to traditional init systems like SysV init, systemd provides faster boot times through parallel startup, better dependency management between services, and continuous service monitoring.

* It also includes built-in logging via journalctl, which makes debugging and system analysis easier.

---

## 🔹 Linux Process States

### 1. New

* The process is being created
* Kernel is setting up its Process Control Block (PCB) and resources
* Example: When you type a command, the shell starts creating a process

---

### 2. Ready

* The process is ready to run but waiting for CPU
* It has all required resources except CPU time
* Sits in the ready queue
* Example: Multiple apps open, waiting for CPU turn

---

### 3. Running

* The process is currently executing on the CPU
* Only limited processes can be in this state at once (based on CPU cores)
* Example: ls command executing, browser loading page

---

### 4. Waiting / Blocked

* The process is waiting for an external event to happen before it can continue
* It is not using CPU during this time

What kind of events?

* I/O operations → waiting for disk read/write (e.g., reading a file)
* User input → waiting for keyboard input
* Network response → waiting for data from server

👉 Example:
When a program reads a file, it pauses until data is fetched from disk

---

### 5. Terminated (Exit)

* Process has finished execution or has been killed
* Kernel cleans up resources (memory, PID, etc.)
* Example: After ls prints output, it exits

---

## 🔹 Top DevOps Troubleshooting Commands

### 1. tail -f

* Real-time log monitoring
* 🔥 Most used in production

Example:
tail -f /var/log/app.log
👉 Used when: app is failing / debugging live issues

---

### 2. grep

* Filter logs for errors

Example:
grep -i error app.log
👉 Used when: finding root cause in huge logs

---

### 3. top / htop

* Check CPU, memory usage
  👉 Used when: server is slow / high CPU

---

### 4. ps aux

* See all running processes
  👉 Used when: checking if service is running

---

### 5. df -h

* Check disk space
  👉 Used when: server crashes / logs not writing

---

### 6. du -sh

* Find which folder is taking space
  👉 Used when: disk full issue

---

### 7. systemctl

* Manage and check services

Example:
systemctl status nginx
👉 Used when: service down
Works with systemd

---

### 8. journalctl

* Check system/service logs

Example:
journalctl -u nginx
👉 Used when: deep debugging of services

---

### 9. netstat / ss

* Check ports and network connections
  👉 Used when: app not reachable

---

### 10. curl

* Test API or service

curl [http://localhost:8080](http://localhost:8080)
👉 Used when: checking if app is responding
