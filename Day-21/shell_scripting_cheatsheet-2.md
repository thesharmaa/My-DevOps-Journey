# Bash Operators and Conditionals

## 1. String Comparisons

Used to compare strings.

### Equal (`=`)

```bash
NAME="Aman"

if [ "$NAME" = "Aman" ]; then
    echo "Match"
fi
```

### Not Equal (`!=`)

```bash
if [ "$NAME" != "John" ]; then
    echo "Different"
fi
```

### String is Empty (`-z`)

```bash
NAME=""

if [ -z "$NAME" ]; then
    echo "String is empty"
fi
```

### String is Not Empty (`-n`)

```bash
NAME="Aman"

if [ -n "$NAME" ]; then
    echo "String is not empty"
fi
```

---

## 2. Integer Comparisons

Used to compare numeric values.

| Operator | Meaning |
|----------|---------|
| `-eq` | Equal to |
| `-ne` | Not equal to |
| `-lt` | Less than |
| `-gt` | Greater than |
| `-le` | Less than or equal to |
| `-ge` | Greater than or equal to |

### Examples

```bash
NUM=10

if [ "$NUM" -eq 10 ]; then
    echo "Equal"
fi
```

```bash
if [ "$NUM" -gt 5 ]; then
    echo "Greater than 5"
fi
```

```bash
if [ "$NUM" -le 20 ]; then
    echo "Less than or equal to 20"
fi
```

---

## 3. File Test Operators

Used to check file and directory properties.

| Operator | Meaning |
|----------|---------|
| `-f` | File exists and is a regular file |
| `-d` | Directory exists |
| `-e` | File or directory exists |
| `-r` | Read permission |
| `-w` | Write permission |
| `-x` | Execute permission |
| `-s` | File exists and is not empty |

### Examples

## File Test Operators

### `-f` → File exists and is a regular file

```bash
if [ -f "notes.txt" ]; then
    echo "notes.txt is a file"
fi
```

**Scenario:** `notes.txt` exists as a file.

---

### `-d` → Directory exists

```bash
if [ -d "/home/aman/Documents" ]; then
    echo "Directory exists"
fi
```

**Scenario:** Checking whether a folder exists.

---

### `-e` → File or directory exists

```bash
if [ -e "notes.txt" ]; then
    echo "Path exists"
fi
```

```bash
if [ -e "/home/aman/Documents" ]; then
    echo "Path exists"
fi
```

**Scenario:** You only care that something exists, not whether it's a file or directory.

---

### `-r` → Read permission

```bash
if [ -r "notes.txt" ]; then
    echo "File is readable"
fi
```

**Scenario:** Current user can read the file.

---

### `-w` → Write permission

```bash
if [ -w "notes.txt" ]; then
    echo "File is writable"
fi
```

**Scenario:** Current user can modify the file.

---

### `-x` → Execute permission

```bash
if [ -x "deploy.sh" ]; then
    echo "Script is executable"
fi
```

**Scenario:** `deploy.sh` has execute permission (`chmod +x deploy.sh`).

---

### `-s` → File exists and is not empty

```bash
if [ -s "log.txt" ]; then
    echo "File contains data"
fi
```

**Scenario:**

- `log.txt` exists ✔️
- Size > 0 bytes ✔️

If the file is empty, the condition is false.

---

## 4. if, elif, else

### Syntax

```bash
if [ condition ]; then
    commands
elif [ another_condition ]; then
    commands
else
    commands
fi
```

### Example

```bash
MARKS=75

if [ "$MARKS" -ge 90 ]; then
    echo "Grade A"
elif [ "$MARKS" -ge 70 ]; then
    echo "Grade B"
else
    echo "Grade C"
fi
```

Output:

```text
Grade B
```

---

## 5. Logical Operators

### AND (`&&`)

Both conditions must be true.

```bash
AGE=25

if [ "$AGE" -gt 18 ] && [ "$AGE" -lt 60 ]; then
    echo "Eligible"
fi
```

### OR (`||`)

At least one condition must be true.

```bash
if [ "$AGE" -lt 18 ] || [ "$AGE" -gt 60 ]; then
    echo "Special Category"
fi
```

### NOT (`!`)

Reverses the condition.

```bash
if ! [ -f "test.txt" ]; then
    echo "File does not exist"
fi
```

---

## 6. Case Statements (`case ... esac`)

Used when checking multiple possible values.

### Syntax

```bash
case $variable in
    pattern1)
        commands
        ;;
    pattern2)
        commands
        ;;
    *)
        default_commands
        ;;
esac
```

### Example

```bash
DAY="Mon"

case $DAY in
    Mon)
        echo "Monday"
        ;;
    Tue)
        echo "Tuesday"
        ;;
    Wed)
        echo "Wednesday"
        ;;
    *)
        echo "Invalid Day"
        ;;
esac
```

Output:

```text
Monday
```

---

## Quick Interview Revision

### String Operators

| Operator | Meaning |
|----------|---------|
| `=` | Equal |
| `!=` | Not Equal |
| `-z` | Empty String |
| `-n` | Non-Empty String |

### Integer Operators

| Operator | Meaning |
|----------|---------|
| `-eq` | Equal |
| `-ne` | Not Equal |
| `-lt` | Less Than |
| `-gt` | Greater Than |
| `-le` | Less Than or Equal |
| `-ge` | Greater Than or Equal |

### File Operators

| Operator | Meaning |
|----------|---------|
| `-f` | File Exists |
| `-d` | Directory Exists |
| `-e` | Exists |
| `-r` | Read Permission |
| `-w` | Write Permission |
| `-x` | Execute Permission |
| `-s` | Not Empty |

### Conditionals

```bash
if [ condition ]; then
elif [ condition ]; then
else
fi
```

### Logical Operators

```bash
&&   # AND
||   # OR
!    # NOT
```

### Case Statement

```bash
case $VAR in
    pattern)
        ;;
    *)
        ;;
esac
```
