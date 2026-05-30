# Task 1: Log Rotation Script
## Create log_rotate.sh that:

## Takes a log directory as an argument (e.g., /var/log/myapp)
## Compresses .log files older than 7 days using gzip
## Deletes .gz files older than 30 days
## Prints how many files were compressed and deleted
## Exits with an error if the directory doesn't exist



```bash
ubuntu@ip-172-31-39-55:~$ cat log_rotate.sh
#!/bin/bash

# Throws error for not providing path to source and path to destination.
if [ $# -eq 0 ]
then
        echo "Usage: ./log_rotate.sh <path to source> <path to destination>"
fi

#takeing variables input
source_dir=$1
destination_dir=$2
timestamp=$(date +'%Y-%m-%d-%H-%M-%S')

#creates backup of given source to given destination
function creating_backup {

        tar -czvf "${destination_dir}/myapp_backup_${timestamp}.tar.gz" "${source_dir}" >/dev/null 2>&1

}


function creating_backup_on_days {

        #copying the log files from source to destination which are 7 days older
        find "${source_dir}" -type f -name "*.log" -mtime +7 -exec cp {} "${destination_dir}" \;

        #number of log files need to be archived
        count=$(find "${source_dir}" -type f -name "*.log" -mtime +7 | wc -l)
        echo "Files to be archived older than 7 days: ${count}"

        #zipping the log files in destination directory using gzip
        find "${destination_dir}" -name "*.log" -exec gzip {} \;

        #deleting the log files from sources direwctory which are 7 days older
        sudo find "${source_dir}" -name "*.log" -mtime +7 -delete

        #number of zipped files older than 30 days needs to be removed
        countzip=$(sudo find "${destination_dir}" -name "*.gzip" -mtime +30 | wc -l)
        echo "Files to be deleted greater thaan 30 days: ${countzip}"

        #deleting the log files already zipped which are 30 days older
        sudo find "${destination_dir}" -name "*.gzip" -mtime +30 -delete  

}



creating_backup_on_days
#creating_backup



```
