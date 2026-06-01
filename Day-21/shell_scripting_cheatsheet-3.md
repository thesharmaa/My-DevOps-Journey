# Bash Loops

## 1. `for` Loop (List-Based)

Used when you know the items to iterate over.

### Syntax

```bash
for item in list
do
    commands
done
```

### Example

```bash
for fruit in Apple Banana Mango
do
    echo "$fruit"
done
```

### Output

```text
Apple
Banana
Mango
```

---

## 2. `for` Loop (C-Style)

Similar to C, Java, and JavaScript loops.

### Syntax

```bash
for (( initialization; condition; increment ))
do
    commands
done
```

### Example

```bash
for (( i=1; i<=5; i++ ))
do
    echo "$i"
done
```

### Output

```text
1
2
3
4
5
```

---

## 3. `while` Loop

Runs while a condition is true.

### Syntax

```bash
while [ condition ]
do
    commands
done
```

### Example

```bash
count=1

while [ "$count" -le 5 ]
do
    echo "$count"
    ((count++))
done
```

### Output

```text
1
2
3
4
5
```

---

## 4. `until` Loop

Runs until a condition becomes true.

### Syntax

```bash
until [ condition ]
do
    commands
done
```

### Example

```bash
count=1

until [ "$count" -gt 5 ]
do
    echo "$count"
    ((count++))
done
```

### Output

```text
1
2
3
4
5
```

### Difference

- `while` → runs while condition is true.
- `until` → runs while condition is false.

---

## 5. Loop Control Statements

### `break`

Exits the loop immediately.

```bash
for (( i=1; i<=10; i++ ))
do
    if [ "$i" -eq 5 ]; then
        break
    fi

    echo "$i"
done
```

### Output

```text
1
2
3
4
```

---

### `continue`

Skips the current iteration.

```bash
for (( i=1; i<=5; i++ ))
do
    if [ "$i" -eq 3 ]; then
        continue
    fi

    echo "$i"
done
```

### Output

```text
1
2
4
5
```

---

## 6. Looping Over Files

Useful for processing multiple files.

### Example

```bash
for file in *.log
do
    echo "Processing $file"
done
```

### Scenario

If the directory contains:

```text
app.log
server.log
error.log
```

Output:

```text
Processing app.log
Processing server.log
Processing error.log
```

---

## 7. Looping Over Command Output

### Example

```bash
cat users.txt | while read line
do
    echo "User: $line"
done
```

### users.txt

```text
Aman
John
David
```

### Output

```text
User: Aman
User: John
User: David
```

---

### Better Practice

Avoid unnecessary `cat`.

```bash
while read line
do
    echo "User: $line"
done < users.txt
```

---

## Quick Interview Revision

### `for` Loop

```bash
for item in list
do
    commands
done
```

### C-Style `for`

```bash
for (( i=1; i<=5; i++ ))
do
    commands
done
```

### `while` Loop

```bash
while [ condition ]
do
    commands
done
```

### `until` Loop

```bash
until [ condition ]
do
    commands
done
```

### Loop Control

```bash
break      # Exit loop
continue   # Skip current iteration
```

### Loop Through Files

```bash
for file in *.log
do
    echo "$file"
done
```

### Read File Line by Line

```bash
while read line
do
    echo "$line"
done < file.txt
```
