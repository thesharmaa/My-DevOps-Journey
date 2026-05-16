## Challenge Tasks

# Task 1: For Loop
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
