# Bash Scripting Basics

## 1. Shebang (`#!/bin/bash`)

### What it does
Tells Linux which interpreter should run the script.

### Example

```bash
#!/bin/bash
echo "Hello World"
```

### Why it matters
Ensures the script runs with Bash even if the default shell is different.

---

## 2. Running a Script

### Make executable

```bash
chmod +x script.sh
```

### Run directly

```bash
./script.sh
```

### Run with Bash

```bash
bash script.sh
```

### Difference

- `./script.sh` uses the shebang.
- `bash script.sh` explicitly runs the script with Bash.

---

## 3. Comments

### Single-line comment

```bash
# This is a comment
echo "Hello"
```

### Inline comment

```bash
echo "Hello"  # Prints Hello
```

### Purpose

Used to explain code and improve readability.

---

## 4. Variables

### Declare a variable

```bash
NAME="Aman"
```

### Use a variable

```bash
echo $NAME
```

### Double quotes (`"$VAR"`)

```bash
echo "Hello $NAME"
```

Output:

```text
Hello Aman
```

Variable gets expanded.

### Single quotes (`'$VAR'`)

```bash
echo '$NAME'
```

Output:

```text
$NAME
```

Prints the variable name literally.

---

## 5. Reading User Input (`read`)

### Example

```bash
echo "Enter your name:"
read NAME
echo "Hello $NAME"
```

### Output

```text
Enter your name:
Aman
Hello Aman
```

---

## 6. Command-Line Arguments

### Script

```bash
#!/bin/bash

echo "Script Name: $0"
echo "First Arg: $1"
echo "Second Arg: $2"
echo "Total Args: $#"
echo "All Args: $@"
```

### Run

```bash
bash script.sh Aman DevOps
```

### Output

```text
Script Name: script.sh
First Arg: Aman
Second Arg: DevOps
Total Args: 2
All Args: Aman DevOps
```

### Important Variables

| Variable | Meaning |
|----------|---------|
| `$0` | Script name |
| `$1`, `$2` | First and second arguments |
| `$#` | Number of arguments |
| `$@` | All arguments |
| `$?` | Exit status of previous command |

### Example of `$?`

```bash
ls
echo $?
```

Output:

```text
0
```

### If a command fails

```bash
ls abc
echo $?
```

Output:

```text
2
```

**Note:** `0` means success. Any non-zero value indicates an error.
