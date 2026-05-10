🐧 Linux File System – Definitions, Examples & Use


🌳 / (Root)
The root directory / is the top-most directory in Linux, and all other files and folders exist inside it. For example, directories like /home, /etc, and /var are all inside /. It is used as the starting point of the entire system, and its significance is very high because if the root is corrupted, the whole operating system can fail.

📁 /home

The /home directory stores personal files of users. For example, /home/aman may contain documents, code, and downloads. It is used to keep user data separate from system files, which is important because it protects your personal data even if system files are modified or updated.

📁 /root

The /root directory is the home folder for the root (admin) user. For example, the system administrator’s files and scripts are stored here. It is used for administrative work and is important because it keeps admin-level files separate and secure from normal users.

📁 /bin

The /bin directory contains essential command binaries like ls, cp, mv, and cat. For example, when you run ls, it actually comes from /bin/ls. It is used to provide basic commands required for system operation, and it is important because these commands are needed even when the system is in a minimal or recovery mode.

📁 /sbin

The /sbin directory contains system administration commands such as reboot and fdisk. For example, sudo reboot uses binaries from this directory. It is used for system control tasks, and its importance lies in managing and maintaining the system, especially by administrators.

📁 /etc Settings app ⚙️

The /etc directory stores configuration files for the system and applications. For example, /etc/hosts manages hostname mappings, and /etc/nginx/nginx.conf configures a web server. It is used to control how the system and services behave, and it is important because even a small change here can affect the entire system.

📁 /var

The /var directory contains variable data that keeps changing, such as logs, cache, and web files. For example, /var/log/syslog stores system logs and /var/www/html stores website files. It is used to track system activity and runtime data, and it is important because it helps in debugging and monitoring.

📁 /usr Installed apps 📱

The /usr directory stores user programs, applications, and libraries. For example, /usr/bin/python3 or /usr/bin/git. It is used to hold most installed software, and it is important because it is the main place from where applications are run.

📁 /tmp

The /tmp directory is used for temporary files created by users or applications. For example, a program may create temporary files in /tmp while running. It is used for short-term storage, and it is important because it helps processes run without storing unnecessary permanent data.

📁 /dev

The /dev directory contains device files that represent hardware. For example, /dev/sda represents a hard disk. It is used to allow the system to interact with hardware devices, and it is important because without it, the system cannot communicate with hardware components.

📁 /proc

The /proc directory is a virtual filesystem that provides real-time system information. For example, /proc/cpuinfo shows CPU details and /proc/meminfo shows memory usage. It is used for monitoring system performance, and it is important for troubleshooting and system analysis.

📁 /boot

The /boot directory contains files needed to start the system, such as the kernel and bootloader. For example, files like vmlinuz and GRUB configuration are stored here. It is used during system startup, and it is important because if these files are missing or corrupted, the system will not boot.

📁 /lib and /lib64

These directories contain shared libraries required by system programs. For example, binaries in /bin depend on libraries stored in /lib. They are used to support program execution, and they are important because without these libraries, many programs will fail to run.

📁 /opt

The /opt directory is used for installing third-party or optional software. For example, applications like Google Chrome or custom software may be installed in /opt. It is used to keep external applications separate, and it is important because it maintains a clean and organized system.

📁 /mnt

The /mnt directory is used as a temporary mount point for storage devices. For example, an admin might mount a disk using /mnt. It is used for manual mounting, and it is important for system administration and troubleshooting.

📁 /media

The /media directory is used to automatically mount external devices like USB drives. For example, a USB may appear in /media/usb. It is used for easy access to external storage, and it is important because it simplifies working with removable devices.
