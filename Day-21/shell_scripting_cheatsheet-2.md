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

### Check if file exists

```bash
if [ -f "test.txt" ]; then
    echo "File exists"
fi
```

### Check if directory exists

```bash
if [ -d "/home/user" ]; then
    echo "Directory exists"
fi
```

### Check if file is readable

```bash
if [ -r "test.txt" ]; then
    echo "Readable"
fi
```

### Check if file is not empty

```bash
if [ -s "test.txt" ]; then
    echo "File contains data"
fi
```

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
