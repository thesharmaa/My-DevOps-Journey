# Bash Error Handling and Debugging

Error handling helps make scripts reliable and easier to troubleshoot.

---

## 1. Exit Codes

Every command returns an exit code.

### Check Exit Status

```bash
ls file.txt

echo $?
```

### Output

```text
0
```

`0` means success.

---

### Failed Command

```bash
ls missing.txt

echo $?
```

### Output

```text
2
```

Non-zero values indicate failure.

---

### Using `exit`

#### Success

```bash
exit 0
```

#### Failure

```bash
exit 1
```

### Example

```bash
if [ ! -f "config.txt" ]; then
    echo "Config file missing"
    exit 1
fi

echo "Config found"
exit 0
```

---

## 2. `set -e`

Exit immediately if any command fails.

### Example Without `set -e`

```bash
#!/bin/bash

mkdir test
cd missing_directory

echo "Script continues"
```

Output:

```text
cd: missing_directory: No such file or directory
Script continues
```

---

### Example With `set -e`

```bash
#!/bin/bash

set -e

mkdir test
cd missing_directory

echo "Script continues"
```

Output:

```text
cd: missing_directory: No such file or directory
```

Script stops immediately.

---

## 3. `set -u`

Treat unset variables as errors.

### Example Without `set -u`

```bash
#!/bin/bash

echo "$USERNAME"
```

Output:

```text
(empty output)
```

---

### Example With `set -u`

```bash
#!/bin/bash

set -u

echo "$USERNAME"
```

Output:

```text
bash: USERNAME: unbound variable
```

Useful for catching typos.

---

## 4. `set -o pipefail`

Makes pipelines fail if any command in the pipeline fails.

### Without `pipefail`

```bash
grep "error" missing.log | wc -l

echo $?
```

Output:

```text
0
```

Pipeline appears successful because `wc` succeeds.

---

### With `pipefail`

```bash
set -o pipefail

grep "error" missing.log | wc -l

echo $?
```

Output:

```text
2
```

The pipeline correctly reports failure.

---

## 5. `set -x`

Debug mode.

Prints each command before executing it.

### Example

```bash
#!/bin/bash

set -x

name="Aman"
echo "$name"
```

Output:

```text
+ name=Aman
+ echo Aman
Aman
```

Useful for troubleshooting scripts.

---

### Disable Debug Mode

```bash
set +x
```

---

## 6. Trap

Execute commands when a script exits or receives a signal.

### Syntax

```bash
trap 'commands' EXIT
```

---

### Example

```bash
cleanup() {
    echo "Cleaning temporary files..."
    rm -f temp.txt
}

trap cleanup EXIT

touch temp.txt

echo "Working..."
```

### Output

```text
Working...
Cleaning temporary files...
```

The cleanup function runs automatically when the script exits.

---

## Real-World Example

```bash
#!/bin/bash

set -euo pipefail

cleanup() {
    echo "Removing temporary files"
    rm -f temp.txt
}

trap cleanup EXIT

touch temp.txt

echo "Processing..."

grep "error" app.log

echo "Done"
```

### What This Does

- `set -e` → stop on command failures
- `set -u` → fail on undefined variables
- `set -o pipefail` → detect failures inside pipelines
- `trap cleanup EXIT` → always run cleanup

This is a common production Bash pattern.

---

# Recommended Production Header

Many DevOps engineers start scripts with:

```bash
#!/bin/bash

set -euo pipefail
```

Meaning:

- `-e` → stop on errors
- `-u` → fail on unset variables
- `pipefail` → detect pipeline failures

For debugging:

```bash
set -euxo pipefail
```

Adds:

```bash
set -x
```

to trace command execution.

---

# Quick Interview Revision

| Command | Purpose |
|----------|----------|
| `$?` | Exit status of previous command |
| `exit 0` | Successful exit |
| `exit 1` | Failure exit |
| `set -e` | Exit on command failure |
| `set -u` | Error on undefined variables |
| `set -o pipefail` | Detect failures in pipelines |
| `set -x` | Debug mode |
| `trap 'cleanup' EXIT` | Run cleanup when script exits |

---

## Interview Answer

> Bash error handling is commonly implemented using `set -euo pipefail`. `set -e` stops execution on errors, `set -u` catches undefined variables, and `set -o pipefail` ensures pipeline failures are detected. `set -x` helps with debugging by tracing commands, while `trap` is used to perform cleanup actions when a script exits.
