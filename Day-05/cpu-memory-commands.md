
🧠 1. ps aux | grep <process>

👉 What it does

Shows all running processes, then filters by name.

ps aux | grep java

🧠 How to read

USER   PID   %CPU   %MEM   COMMAND
root   1234  80.0   60.0   java

* %CPU → CPU usage
* %MEM → memory usage
* PID → process ID

⸻

🚨 Real Scenario

👉 “App is slow”

You run:

ps aux | grep java

Output:

java  1234  150% CPU

👉 Insight:

* One process is hogging CPU

✔️ Next step:

* Use top or pidstat

⸻

⚡ 2. pgrep <name>

👉 What it does

Quickly gives PID(s) of a process

pgrep java

Output:

1234
5678

⸻

🧠 Why it’s useful

Instead of:

ps aux | grep java

👉 Just:

pgrep java

✔️ Faster + script-friendly

⸻

🚨 Real Scenario

👉 You want to restart a service:

kill -9 $(pgrep java)

✔️ Kills all Java processes instantly

⸻

📊 3. pidstat 1

👉 What it does

Shows per-process resource usage in real time

pidstat 1

⸻

🧠 Output example

PID   %CPU   %MEM   COMMAND
1234  90.0   40.0   java
2345   5.0   10.0   nginx

⸻

🚨 Real Scenario (VERY IMPORTANT)

👉 Problem:

* CPU high
* But top keeps changing processes

Run:

pidstat 1

👉 You discover:

* Same PID consistently using CPU

✔️ Insight:

* Stable CPU hog (not spikes)

⸻

🔪 4. kill -9 <PID>

👉 What it does

Forcefully kills a process

kill -9 1234

⸻

🧠 Important

* -9 = SIGKILL (no cleanup ❗)
* Process dies immediately

⸻

🚨 Real Scenario

👉 Memory leak:

ps aux --sort=-%mem | head

Output:

PID  %MEM  COMMAND
1234 80%   java

👉 System swapping, slow

✔️ Action:

kill -9 1234

👉 Result:

* Memory freed
* System stable

⸻

⚠️ Interview Tip

👉 Always say:

“Use kill -9 as last resort”

⸻

🎛️ 5. nice / renice

👉 What it does

Controls process priority (CPU scheduling)

⸻

🧠 Priority concept

* Lower nice value → higher priority
* Higher nice value → lower priority

Range:

-20 (highest priority) → 19 (lowest priority)

⸻

✅ Example

Start low priority process:

nice -n 10 python script.py

⸻

Change priority of running process:

renice 10 -p 1234

⸻

🚨 Real Scenario

👉 Problem:

* Backup job consuming CPU
* App performance degraded

Check:

pidstat 1

Find:

backup.sh using 70% CPU

✔️ Solution:

renice 15 -p <backup_PID>

👉 Result:

* Backup slows down
* App gets CPU

⸻

🔥 Full Real Troubleshooting Flow

🚨 Scenario: “Server slow”

⸻

Step 1: Find process

ps aux --sort=-%cpu | head

👉 Identify top CPU consumer

⸻

Step 2: Confirm

pidstat 1

👉 Check if consistent

⸻

Step 3: Get PID quickly

pgrep java

⸻

Step 4: Decide action

Situation	Action
Critical app stuck	kill -9
Non-critical heavy job	renice
Unknown process	Investigate first

⸻

🎯 Interview Answer (clean)

👉 Say this:

“These commands help in process-level troubleshooting. ps and pgrep identify processes, pidstat shows real-time usage, kill is used to stop problematic processes, and nice/renice helps control CPU priority to balance workloads.”

⸻

⚡ One-line memory

* ps → find process
* pgrep → get PID fast
* pidstat → who is consuming resources
* kill -9 → emergency stop
* renice → control priority
