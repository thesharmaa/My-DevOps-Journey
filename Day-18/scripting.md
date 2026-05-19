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
