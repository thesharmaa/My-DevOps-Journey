# Challenge Tasks

## Task 1: For Loop
Create for_loop.sh that:
Loops through a list of 5 fruits and prints each one
```bash
#!/bin/bash
fruits=("apple" "mango" "banana")
for fruit in "${fruits[@]}"
do 
  echo "$fruit"
done
```

Create count.sh that:
Prints numbers 1 to 10 using a for loop
```bash
#!/bin/bash
for (( num=1 : num <= 10 : num++ ))
do 
  echo $num
done
```

## Task 2: While Loop
Create countdown.sh that:
Takes a number from the user
Counts down to 0 using a while loop
Prints "Done!" at the end

```bash
num=5
while (( num >= 0 ))
do
 echo "$num"
 (( num-- ))
done
echo "Done!"
```

## Task 3: Command-Line Arguments
Create greet.sh that:
Accepts a name as $1
Prints Hello, <name>!
If no argument is passed, prints "Usage: ./greet.sh "
```bash
#!/bin/bash
name=$1
if [ -z $name ]
then
echo "Usage:./greet.sh"
else
echo "Hello, $name"
fi
```

Create args_demo.sh that:
Prints total number of arguments $hash
Prints all arguments $@
Prints the script name $0

```bash
#!/bin/bash
echo "Total number of args passed: $#"
echo "Args passed: $@"
echo "Script name is : $0"
```


## Task 4: Install Packages via Script
Create install_packages.sh that:
Defines a list of packages: nginx, curl, wget
Loops through the list
Checks if each package is installed (use dpkg -s or rpm -q)
Installs it if missing, skips if already present
Prints status for each package

```bash
#!/bin/bash
packages=("nginx" "wget" "curl")
for package in "${packages[@]}" 
do 
if dpkg -s "$package" >/dev/null 2>&1 
then 
echo ""$package" is already installed" 
else
echo ""$package" is not installed"
echo "Installing the "$package""
sudo apt-get update -y >/dev/null
sudo apt-get install "$package" -y >/dev/null
echo ""$package" is installed"
fi
done
```

## Task 5: Error Handling
Create safe_script.sh that:
Uses set -e at the top (exit on error)
Tries to create a directory /tmp/devops-test
Tries to navigate into it
Creates a file inside
Uses || operator to print an error if any step fails
Example:
mkdir /tmp/devops-test || echo "Directory already exists"
```bash
#!/bin/bash
mkdir -p /tmp/devops-test/ || echo "Directory already exist"
cd /tmp/devops-test/ || echo "Unable to navigate to directory"
touch test.txt || echo "Unable to create the text file"
```

## 2. Modify your install_packages.sh to check if the script is being run as root — exit with a message if not.
```bash
#!/bin/bash

if [ "$EUID" -ne 0 ]
then
    echo "Please run with sudo"
    exit 1
fi
packages=("nginx" "wget" "curl")
for package in "${packages[@]}" 
do 
if dpkg -s "$package" >/dev/null 2>&1 
then 
echo ""$package" is already installed" 
else
echo ""$package" is not installed"
echo "Installing the "$package""
sudo apt-get update -y >/dev/null
sudo apt-get install "$package" -y >/dev/null
echo ""$package" is installed"
fi
done

```

