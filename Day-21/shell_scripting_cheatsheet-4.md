# Bash Functions

## 1. Defining a Function

Functions allow you to group reusable code into a single block.

### Syntax

```bash
function_name() {
    commands
}
```

### Example

```bash
greet() {
    echo "Hello World"
}
```

---

## 2. Calling a Function

Simply use the function name.

### Example

```bash
greet() {
    echo "Hello World"
}

greet
```

### Output

```text
Hello World
```

---

## 3. Passing Arguments to Functions

Arguments are accessed using `$1`, `$2`, etc., just like script arguments.

### Example

```bash
greet() {
    echo "Hello $1"
}

greet Aman
```

### Output

```text
Hello Aman
```

### Multiple Arguments

```bash
introduce() {
    echo "Name: $1"
    echo "Role: $2"
}

introduce Aman DevOps
```

### Output

```text
Name: Aman
Role: DevOps
```

---

## 4. Return Values

### Using `return`

- `return` is used to return an exit status.
- Valid range: `0 - 255`.
- Commonly used for success/failure.

### Example

```bash
check_number() {
    if [ "$1" -gt 0 ]; then
        return 0
    else
        return 1
    fi
}

check_number 10

echo $?
```

### Output

```text
0
```

### Example

```bash
check_number -5

echo $?
```

### Output

```text
1
```

---

### Using `echo`

To return actual data from a function, use `echo`.

### Example

```bash
get_name() {
    echo "Aman"
}

name=$(get_name)

echo "$name"
```

### Output

```text
Aman
```

### Why Use `echo`?

`return` can only return numbers (0-255).

```bash
return 100
```

Valid ✅

```bash
return "Aman"
```

Invalid ❌

For strings or command output, use `echo`.

---

## 5. Local Variables

By default, variables inside a function are global.

### Example (Global Variable)

```bash
greet() {
    name="Aman"
}

greet

echo "$name"
```

### Output

```text
Aman
```

The variable is accessible outside the function.

---

### Using `local`

```bash
greet() {
    local name="Aman"
    echo "$name"
}

greet

echo "$name"
```

### Output

```text
Aman
```

```text
(empty)
```

### Why Use `local`?

Prevents variables inside functions from affecting variables outside the function.

---

## Complete Example

```bash
greet() {
    local name="$1"

    if [ -n "$name" ]; then
        echo "Hello $name"
        return 0
    else
        echo "Name is required"
        return 1
    fi
}

greet Aman

echo "Exit Status: $?"
```

### Output

```text
Hello Aman
Exit Status: 0
```

---

## Quick Interview Revision

### Define Function

```bash
function_name() {
    commands
}
```

### Call Function

```bash
function_name
```

### Function Arguments

```bash
$1
$2
$#
$@
```

### Return Status

```bash
return 0
return 1
```

### Return Data

```bash
echo "value"

result=$(function_name)
```

### Local Variable

```bash
local variable_name="value"
```

### Interview Answer

> Functions in Bash are reusable blocks of code defined using `function_name() {}`. Arguments are accessed with `$1`, `$2`, etc. `return` is used to send an exit status (0–255), while `echo` is commonly used to return actual data. Variables can be limited to a function's scope using the `local` keyword.
