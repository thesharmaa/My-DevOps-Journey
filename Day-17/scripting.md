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
