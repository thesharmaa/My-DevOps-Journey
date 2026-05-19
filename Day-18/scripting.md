## Task 1: Basic Functions
### Create functions.sh with:
### A function greet that takes a name as argument and prints Hello, <name>!
### A function add that takes two numbers and prints their sum
### Call both functions from the script

```bash
set -euo pipefail
#!/bin/bash
greet() {
    local name=$1
    echo "Hello, $name"
}

greet Aman
```


```bash
set -euo pipefail
#!/bin/bash
add() {
    local num1=$1
    local num2=$2
    echo "Sum of $num1 and $num2 is: "$(($num1+$num2))
}

add 2 5
```

## Task 2: Functions with Return Values
### Create disk_check.sh with:
### function check_disk that checks disk usage of / using df -h
### function check_memory that checks free memory using free -h
### main section that calls both and prints the results


```bash
set -euo pipefail
#!/bin/bash
check_disk() {
    df -h
}
function check_memory() {
    free -h
}
check_disk
check_memory
```


## Task 3: Strict Mode — set -euo pipefail
### Create strict_demo.sh with set -euo pipefail at the top
### Try using an undefined variable — what happens with set -u?
```bash
./strict_demo.sh: line 6: name: unbound variable

set -u: catches typos and any missing variable
```
### Try a command that fails — what happens with set -e?
```bash
mkdir test
cd testt
./strict_demo.sh: line 6: cd: testt: No such file or directory
set -e: exit the script immediately if any command fails
```
### Try a piped command where one part fails — what happens with set -o pipefail?
```bash
touch file.txt
cat file.txt | grep "Aman"
cat: fille.txt: No such file or directory

set -o pipefail: makes bash detect failure inside pipelines instead of checking only the last command.
```



## Task 4: Local Variables
Create local_demo.sh with:
A function that uses local keyword for variables
Show that local variables don't leak outside the function
Compare with a function that uses regular variables

```bash
#!/bin/bash
set -euo pipefail

name="Aman"
my_name() {
  name=$1
  echo "My name is, $name"
}

my_name Rahul
echo $name // Rahul
So this changes the local variable name to "Rahul".

name="Aman"
my_name() {
  local name=$1
  echo "My name is, $name"
}

my_name Rahul
echo $name // Aman
Correct one
```

## Task 5: Build a Script — System Info Reporter
Create system_info.sh that uses functions for everything:

A function to print hostname and OS info
A function to print uptime
A function to print disk usage (top 5 by size)
A function to print memory usage
A function to print top 5 CPU-consuming processes
A main function that calls all of the above with section headers
Use set -euo pipefail at the top
```bash
#!/bin/bash

set -euo pipefail

hostname_&_OS_info() {
    echo ".....Your IP Address....."
    hostname -I
    echo ".....Your Hostname....."
    hostname
    echo ".....Your OS info....."
    cat /etc/os-release
}

load_average(){
    echo "========Load average========"
    uptime
}

disk_usage(){
    echo "========Disk Usage========"
    df -h | sort -hr -k2
}

memory_usage(){
    echo "========Memory Usage========"
    free -m
}

top_5_CPU_consuming(){
    echo "========CPU Consuming Process========"
    ps -eo pid,ppid,cmd,%cpu --sort=-%cpu |head -6
}

hostname_&_OS_info
load_average
disk_usage
memory_usage
top_5_CPU_consuming
memory_usage

-- INSERT --

```









