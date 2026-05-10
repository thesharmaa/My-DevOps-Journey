# touch vs vim
touch is used to create an empty file or update timestamps, whereas vim is a command-line text editor used to create, edit, and manage file content interactively

# How to view script.sh in vim read-only mode
"vim -R filename" is used to open a file in read-only mode in Vim. It allows users to view the file content without accidentally modifying it.


# Task 1: Create Files
- Create empty file devops.txt using touch
- Create notes.txt with some content using cat or echo
- Create script.sh using vim with content: echo "Hello DevOps"
<img width="379" height="152" alt="image" src="https://github.com/user-attachments/assets/06df4451-4f35-432e-b3e1-a590d887056f" />

# Task 2: Read Files
- Read notes.txt using cat
- View script.sh in vim read-only mode
- Display first 5 lines of /etc/passwd using head
- Display last 5 lines of /etc/passwd using tail
<img width="466" height="194" alt="image" src="https://github.com/user-attachments/assets/20963af9-59bb-4366-b116-9c25c88417c7" />

# Task 3: Understand Permissions
- r = read (4), w = write (2), x = execute (1)
- What are current permissions? Who can read/write/execute?
<img width="466" height="54" alt="image" src="https://github.com/user-attachments/assets/cf2a51b0-220f-4897-a0b0-1f968f31f741" />
- The `ubuntu` user and group have read and write access to `devops.txt`, `notes.txt`, and `scripts.sh`, while other users only have read permission for these files.



