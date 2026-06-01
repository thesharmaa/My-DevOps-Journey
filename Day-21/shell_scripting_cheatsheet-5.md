# Bash Text Processing Commands

## 1. grep

Search for patterns in files or command output.

### Syntax

```bash
grep [options] pattern file
```

### Common Flags

| Flag | Meaning |
|--------|---------|
| `-i` | Ignore case |
| `-r` | Recursive search |
| `-c` | Count matches |
| `-n` | Show line numbers |
| `-v` | Invert match (exclude matches) |
| `-E` | Extended regex |

### Examples

#### Search for a pattern

```bash
grep "error" app.log
```

#### Ignore case

```bash
grep -i "error" app.log
```

#### Recursive search

```bash
grep -r "error" /var/log
```

#### Count matches

```bash
grep -c "error" app.log
```

#### Show line numbers

```bash
grep -n "error" app.log
```

#### Exclude matching lines

```bash
grep -v "error" app.log
```

#### Extended Regex

```bash
grep -E "error|warning" app.log
```

---

## 2. awk

Powerful text-processing tool for working with columns and patterns.

### Print Columns

```bash
awk '{print $1}' users.txt
```

Print first column.

```bash
awk '{print $1, $3}' users.txt
```

Print first and third columns.

---

### Field Separator

Default separator = whitespace.

Custom separator:

```bash
awk -F: '{print $1}' /etc/passwd
```

Print username from `/etc/passwd`.

---

### Pattern Matching

```bash
awk '/error/ {print}' app.log
```

Print lines containing "error".

---

### BEGIN and END

```bash
awk '
BEGIN {print "Start"}
{print $1}
END {print "End"}
' file.txt
```

Output:

```text
Start
...
End
```

---

## 3. sed

Stream editor used for search, replace, and editing text.

### Substitute Text

```bash
sed 's/error/warning/' file.txt
```

Replace first occurrence per line.

### Replace All Occurrences

```bash
sed 's/error/warning/g' file.txt
```

---

### Delete Line

Delete line 3:

```bash
sed '3d' file.txt
```

Delete blank lines:

```bash
sed '/^$/d' file.txt
```

---

### In-Place Edit

```bash
sed -i 's/error/warning/g' file.txt
```

Modify file directly.

---

## 4. cut

Extract columns from text.

### By Delimiter

```bash
cut -d: -f1 /etc/passwd
```

Output:

```text
root
user1
user2
```

Extract first field separated by `:`.

---

### Multiple Fields

```bash
cut -d: -f1,3 /etc/passwd
```

Print fields 1 and 3.

---

## 5. sort

Sort lines alphabetically or numerically.

### Alphabetical Sort

```bash
sort names.txt
```

---

### Numerical Sort

```bash
sort -n numbers.txt
```

---

### Reverse Sort

```bash
sort -r names.txt
```

---

### Unique Sort

```bash
sort -u names.txt
```

Sort and remove duplicates.

---

## 6. uniq

Remove duplicate adjacent lines.

### Remove Duplicates

```bash
uniq names.txt
```

---

### Count Occurrences

```bash
uniq -c names.txt
```

Output:

```text
3 Aman
2 John
```

---

### Common Usage

```bash
sort names.txt | uniq
```

or

```bash
sort names.txt | uniq -c
```

---

## 7. tr

Translate or delete characters.

### Convert Lowercase to Uppercase

```bash
echo "hello" | tr 'a-z' 'A-Z'
```

Output:

```text
HELLO
```

---

### Delete Characters

```bash
echo "hello123" | tr -d '0-9'
```

Output:

```text
hello
```

---

## 8. wc

Count lines, words, and characters.

### Count Lines

```bash
wc -l file.txt
```

---

### Count Words

```bash
wc -w file.txt
```

---

### Count Characters

```bash
wc -m file.txt
```

---

### All Counts

```bash
wc file.txt
```

Output:

```text
10 50 300 file.txt
```

(lines words bytes)

---

## 9. head

Display first N lines.

### First 10 Lines

```bash
head file.txt
```

---

### First 5 Lines

```bash
head -n 5 file.txt
```

---

## 10. tail

Display last N lines.

### Last 10 Lines

```bash
tail file.txt
```

---

### Last 5 Lines

```bash
tail -n 5 file.txt
```

---

### Follow Mode (Live Logs)

```bash
tail -f app.log
```

Continuously shows new log entries.

Useful for monitoring applications.

---

# Common DevOps Examples

### Find Errors in Logs

```bash
grep -i "error" app.log
```

### Count Errors

```bash
grep -c "error" app.log
```

### Show Last 50 Log Lines

```bash
tail -n 50 app.log
```

### Monitor Logs Live

```bash
tail -f app.log
```

### Extract Usernames

```bash
cut -d: -f1 /etc/passwd
```

### Find Top Duplicate Entries

```bash
sort users.txt | uniq -c
```

### Convert Text to Uppercase

```bash
echo "devops" | tr 'a-z' 'A-Z'
```

---

# Quick Interview Revision

| Command | Purpose |
|----------|----------|
| `grep` | Search patterns |
| `awk` | Process columns and text |
| `sed` | Search and replace |
| `cut` | Extract fields |
| `sort` | Sort lines |
| `uniq` | Remove/count duplicates |
| `tr` | Translate/delete characters |
| `wc` | Count lines, words, chars |
| `head` | First N lines |
| `tail` | Last N lines / monitor logs |
