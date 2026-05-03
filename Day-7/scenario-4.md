A script at /home/user/backup.sh is not executing.
When you run it: ./backup.sh
You get: "Permission denied"

What commands would you use to fix this?

Answer:The error indicates missing execute permission. I would use chmod +x backup.sh to make it executable and then run it using ./backup.sh. Alternatively, I can run it using bash backup.sh

# Check permissions
ls -l backup.sh

# Add execute permission
chmod +x backup.sh  // rwxr-xr-x or
else chmod 700 backup.sh // rwx------

# Run script
./backup.sh
