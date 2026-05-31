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



# Task 2: Server Backup Script
## Create backup.sh that:

## Takes a source directory and backup destination as arguments
## Creates a timestamped .tar.gz archive (e.g., backup-2026-02-08.tar.gz)
## Verifies the archive was created successfully
## Prints archive name and size
## Deletes backups older than 14 days from the destination
## Handles errors — exit if source doesn't exist

```bash
#!/bin/bash


source=$1
destination=$2
if [ ! "${source}" ]
then
echo "Error: Source directory does not exist"
exit 1
fi



timestamp=$(date +'%Y-%m-%d-%H-%M-%S')

#archiveing and compressing the file
backup_file="${destination}/backup-${timestamp}.tar.gz"
tar -cvzf "${backup_file}" "${source}" >/dev/null 2>&1

if [ -f "${backup_file}" ]
then
        echo "Success: Backup file created successfully"
        echo "Archive name: "$(basename $backup_file)""
        echo "Sixes: $(du -h "${backup_file}" | awk '{print $1}')"
else
        echo "Backup failed"
        exit 1
fi

find "${destination}" -name "*.tar.gz" -mtime +14 -delete

```


# Task 4: Combine — Scheduled Maintenance Script
## Create maintenance.sh that:

## alls your log rotation function
## Calls your backup function
## Logs all output to /var/log/maintenance.log with timestamps
## Write the cron entry to run it daily at 1 AM




```bash
#!/bin/bash


log_file="/var/log/maintenance.log"

echo "========$(date) Starting maintenance ========"

#Calling log_rotation script
echo "$(date +'%Y-%m-%d-%H-%M-%S') Running log rotation" >> "${log_file}"
echo $?
echo ${log_file}
bash /home/ubuntu/log_rotate.sh /var/log/myapp /home/ubuntu/backups >> "${log_file}" 2>&1

#calling backup script
bash /home/ubuntu/backup.sh /home/ubuntu/files /home/ubuntu/files_backups >> "${log_file}" 2>&1

echo "========= $(date +'%Y-%m-$d-%H-%M-%S') Maintenance completed ========"
echo " ">> "${log_file}"

```









