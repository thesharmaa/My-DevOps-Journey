# 🧠 Linux `top` vs `htop`

Both are **real-time system monitoring tools** used to check:

* CPU usage
* Memory usage
* Running processes
* System load

👉 Difference:

* `top` = default, basic, older tool
* `htop` = advanced, interactive, user-friendly version

---

# 🔵 1. `top` Command 
## ▶ What it is

top (Linux process monitor) is a **built-in system monitor tool** that shows running processes and system stats in real time.

It comes pre-installed on almost all Linux systems.

---

## 📊 `top` Output Explained

When you run:

```bash
top
```

You see 2 main sections:

---

## 🟡 A. System Summary (Top Area)

Example:

```
top - 14:20:01 up 2 days,  3 users,  load average: 0.45, 0.60, 0.70
Tasks: 200 total, 1 running, 199 sleeping
%Cpu(s): 10.5 us, 2.3 sy, 0.0 ni, 87.2 id
MiB Mem :  8000 total,  2000 free,  5000 used, 1000 buff/cache
```

### 🔍 Meaning:

| Field        | Meaning                     |
| ------------ | --------------------------- |
| uptime       | How long system is running  |
| load average | CPU demand (1, 5, 15 min), average number of processes that are either running or waiting  |
| tasks        | total processes             |
| CPU %        | how CPU is being used       |
| memory       | RAM usage (used/free/cache) |

---

## 🟢 B. Process List (Bottom Area)

| Column  | Meaning             |
| ------- | ------------------- |
| PID     | Process ID          |
| USER    | who started process |
| %CPU    | CPU usage           |
| %MEM    | RAM usage           |
| COMMAND | process name        |

---

## ⚠️ Important interpretation

* High `%CPU` = process is heavy on CPU
* High `%MEM` = process consuming RAM
* Zombie processes = broken/finished incorrectly

---

## 🛠️ Basic troubleshooting using `top`

### 🔥 System slow?

Check:

* CPU > 90% → CPU bottleneck
* load average > CPU cores → overload

### 🔥 Memory issue?

Check:

* low “free memory”
* high “swap usage”

### 🔥 Find culprit process

Sort:

* Press `P` → CPU sort
* Press `M` → Memory sort

---

# 🟣 2. `htop` Command (Modern Interactive Tool)

## ▶ What it is

htop (Linux process viewer) is an **interactive, improved version of top**

It gives:

* colors
* mouse support
* scroll
* tree view
* easier process control

📌 It is NOT always pre-installed

Install:

```bash
sudo apt install htop
```

Run:

```bash
htop
```

---

## 📊 `htop` Output Explained

### 🟡 1. CPU Bars (Top)

* Each CPU core shown separately
* Color coded usage

👉 Example meaning:

* Green = user processes
* Red = kernel/system load
* Blue = low priority tasks

---

### 🟢 2. Memory + Swap Bars

Shows:

* RAM usage
* Cache usage
* Swap usage

⚠️ Important:
Linux uses RAM for caching → so “used memory” is NOT always bad.

---

### 🔵 3. Process List (Middle)

Same as top but better:

| Column  | Meaning        |
| ------- | -------------- |
| PID     | process ID     |
| CPU%    | CPU usage      |
| MEM%    | RAM usage      |
| TIME+   | total CPU time |
| Command | full command   |

---

## ⚡ Key Features of htop

✔ Scroll up/down
✔ Search process (`F3`)
✔ Kill process (`F9`)
✔ Tree view (`F5`)
✔ Filter processes (`F4`)
✔ Mouse support

👉 You can directly manage processes without typing commands.

---

## 🛠️ Troubleshooting using htop

### 🔥 CPU high usage

* Sort by CPU
* Find top process
* Kill or restart process

---

### 🔥 Memory leak

* Sort by MEM%
* Look for continuously increasing process

---

### 🔥 System freeze

* Check load average
* If > CPU cores → system overloaded

---

### 🔥 Zombie processes

* Shown as `Z`
* Means parent process not cleaned properly

---

# ⚖️ `top` vs `htop` (Quick Comparison)

| Feature       | top          | htop        |
| ------------- | ------------ | ----------- |
| Interface     | Text-only    | Color + UI  |
| Mouse support | ❌            | ✔           |
| Scrolling     | ❌            | ✔           |
| Process tree  | ❌            | ✔           |
| Kill process  | complex      | simple (F9) |
| Sorting       | limited keys | interactive |
| Default tool  | ✔            | ❌           |


