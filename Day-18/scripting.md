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





















