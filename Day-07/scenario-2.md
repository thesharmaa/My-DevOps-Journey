🔹 Step 1: Check system load
uptime
👉 Why: To check system load average and confirm if the server is under high load

🔹 Step 2: Check real-time CPU usage
top → Is it CPU, memory, or something else?
👉 Why: To view processes consuming high CPU in real time

🔹 Step 3: List top CPU-consuming processes (snapshot view)
ps aux --sort=-%cpu | head -10 → Who is the culprit?
👉 Why: To quickly identify processes consuming highest CPU without interactive view

🔹 Step 4: Drill down into specific process (PID level)
ps -p <PID> -o pid,ppid,%cpu,%mem,cmd
👉 Why: To analyze details of the high CPU process and understand what it is doing

