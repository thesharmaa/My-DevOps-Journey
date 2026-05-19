## Task 1: Basic Functions
Create functions.sh with:
A function greet that takes a name as argument and prints Hello, <name>!
A function add that takes two numbers and prints their sum
Call both functions from the script

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
