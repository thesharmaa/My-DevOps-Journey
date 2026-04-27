💾 Disk & Storage Troubleshooting

👉 Problem statements usually look like:

* “Disk is full”
* “System is slow but CPU is fine”
* “App suddenly stopped writing logs”

⸻

🔹 1. df -h → Disk space usage

df -h

🧠 What it shows

Filesystem   Size  Used  Avail  Use%
/dev/sda1     50G   48G   2G     96%

👉 Key column: Use%

⸻

🚨 Real Scenario

👉 App error:

“No space left on device”

Run:

df -h

👉 You see:

* / = 96% full ❗

✔️ Insight:
👉 Disk almost full → writes will fail

⸻

🔹 2. du -sh * → Folder-wise usage

du -sh *

🧠 What it does

* Shows size of each folder in current directory

Example:

2G   logs/
10G  backups/
500M temp/

⸻

🚨 Real Scenario

👉 After df -h shows disk full

Go inside:

cd /var
du -sh *

👉 Find:

* logs/ = 20GB ❗

✔️ Insight:
👉 Logs are filling disk

⸻

🔹 3. lsblk → Disk & partition structure

lsblk

🧠 Output

NAME   SIZE TYPE MOUNTPOINT
sda    100G disk
├─sda1  50G part /
├─sda2  50G part /data

⸻

🚨 Real Scenario

👉 Disk full on /

But:

* /data has free space

✔️ Insight:
👉 Problem is partition-specific, not entire disk

⸻

🔹 4. find / -size +500M → Find large files

find / -size +500M

🧠 What it does

👉 Finds files larger than 500MB

⸻

🚨 Real Scenario

👉 You don’t know what’s filling disk

Run:

find / -size +1G

👉 Output:

/var/log/app.log (5GB)
/tmp/dump.hprof (10GB)

✔️ Insight:
👉 Huge dump/log files eating space

⸻

🔹 5. iostat → Disk performance

iostat -xz 1

🧠 Key fields

Field	Meaning
%util	Disk usage
await	wait time
r/s, w/s	reads/writes per sec

⸻

🚨 Real Scenario

👉 Problem:

* System slow
* CPU low
* Memory fine

Run:

iostat -xz 1

👉 Output:

%util = 100%
await = 200ms

✔️ Insight:
👉 Disk is fully busy → bottleneck

⸻

🔥 FULL REAL TROUBLESHOOTING FLOW

🚨 Scenario: “System is slow”

⸻

Step 1: Check disk space

df -h

👉 If full → go next

⸻

Step 2: Find heavy folders

du -sh *

⸻

Step 3: Find exact large files

find / -size +1G

⸻

Step 4: Check disk structure

lsblk

⸻

Step 5: Check disk performance

iostat -xz 1

⸻

🧠 Two types of disk problems

⸻

🔴 1. Disk FULL

👉 Symptoms:

* “No space left”
* App crashes

✔️ Use:

* df -h
* du -sh
* find

⸻

🔴 2. Disk SLOW

👉 Symptoms:

* High wa
* Slow system

✔️ Use:

* iostat

⸻

🎯 Interview Answer

👉 Say this:

“For disk issues, df checks space, du identifies large directories, find locates big files, lsblk shows disk structure, and iostat helps detect performance bottlenecks.”

⸻

⚡ One-line mental model

👉

* df → “Is disk full?”
* du → “Which folder?”
* find → “Which file?”
* lsblk → “Which disk?”
* iostat → “Is disk slow?”
