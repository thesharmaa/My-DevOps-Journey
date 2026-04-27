

🔵 1. top – Live system view (CPU + Memory + Processes)

🧠 What it shows:

* CPU usage
* Memory usage
* Running processes
* Load on system

📊 Key fields:

* %Cpu(s)
    * us → user CPU (apps)
    * sy → system CPU (kernel)
    * wa → I/O wait (VERY IMPORTANT)
* load average → system pressure (not just CPU)
* Process table:
    * %CPU → CPU usage per process
    * %MEM → memory usage
    * RES → actual RAM used

🔥 How to think:

“Who is consuming resources right now?”

⸻

🔵 2. htop – Better top

🧠 Extra features:

* Colored CPU bars
* Tree view (parent-child processes)
* Kill process easily (F9)
* Sort interactively

🔥 When to use:

When debugging faster and visually

⸻

🔵 3. uptime – Load average

📊 Output:

load average: 1.20, 2.10, 3.00

🧠 Meaning:

* 1 min, 5 min, 15 min load
* Compare with CPU cores

👉 Example:

* 4 core CPU:
    * Load 4 = fully utilized
    * Load >4 = overloaded

⚠️ Important:

Load includes CPU + I/O wait (not just CPU)

⸻

🔵 4. free -m – Memory check

📊 Output:

total used free buff/cache available

🧠 Key points:

* available → REAL usable memory
* used ≠ actually used (Linux caches)

🔥 Red flag:

* Low available memory
* High swap usage

⸻

🔵 5. vmstat 1 – Real-time system behavior

📊 Key columns:

* r → running processes (CPU queue)
* b → blocked processes (waiting for I/O)
* si/so → swap in/out
* wa → I/O wait
* us/sy → CPU usage

🧠 Interpretation:

* r > CPU cores → CPU bottleneck
* b > 0 → I/O bottleneck
* si/so > 0 → memory issue

⸻

🔵 6. iostat -xz 1 – Disk bottleneck detector

📊 Key fields:

* %util → disk busy %
* await → wait time (IMPORTANT)
* r/s, w/s → read/write ops
* avgqu-sz → queue size

🧠 Interpretation:

* %util ~ 100% → disk saturated
* await high → slow disk
* avgqu-sz high → queue buildup

⸻

⚡ HOW TO THINK (INTERVIEW GOLD)

👉 Always follow this flow:

1. uptime → is system under load?
2. top/htop → who is causing it?
3. vmstat → CPU / Memory / I/O?
4. free → memory issue?
5. iostat → disk issue?

Refine for github so that i can commit it