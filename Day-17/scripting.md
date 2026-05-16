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
