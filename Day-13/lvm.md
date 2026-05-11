# Linux LVM Hands-on Lab on AWS EC2 🚀

Today I practiced Linux Logical Volume Management (LVM) using multiple AWS EBS volumes attached to an EC2 instance.

This lab helped me understand:
- PV, VG, LV concepts
- filesystem formatting
- mounting storage
- extending storage dynamically
- difference between `lsblk` and `df -h`
- how LVM abstracts physical disks

---

# Task 1: Check Current Storage

Check existing disks, PVs, VGs, LVs, and mounted filesystems.

```bash
lsblk
pvs
vgs
lvs
df -h
Task 2: Create Physical Volumes (PV)

Initialize attached EBS disks as LVM Physical Volumes.

pvcreate /dev/nvme1n1
pvcreate /dev/nvme2n1
pvcreate /dev/nvme3n1

Verify:

pvs
Task 3: Create Volume Group (VG)

Combine multiple PVs into one storage pool.

vgcreate devops-vg /dev/nvme1n1 /dev/nvme2n1 /dev/nvme3n1

Verify:

vgs
Task 4: Create Logical Volume (LV)

Create usable logical storage from the VG.

lvcreate -L 500M -n app-data devops-vg

Verify:

lvs

Check hierarchy:

lsblk
Task 5: Format and Mount the LV

Create filesystem on the LV.

mkfs.ext4 /dev/devops-vg/app-data

Create mount point:

mkdir -p /mnt/app-data

Mount the LV:

mount /dev/devops-vg/app-data /mnt/app-data

Verify mounted filesystem:

df -h /mnt/app-data
Task 6: Extend the Logical Volume

Increase LV size dynamically.

lvextend -L +200M /dev/devops-vg/app-data

At this stage:

lsblk showed increased LV size
but df -h still showed old filesystem size

This was because:

LV size increased
filesystem size did not increase yet

Resize filesystem:

resize2fs /dev/devops-vg/app-data

Verify again:

df -h /mnt/app-data
Key Learnings 💡
1. Difference Between lsblk and df -h
lsblk

Shows:

disks
partitions
LVM hierarchy
block device sizes
df -h

Shows:

mounted filesystem usable space
2. Important LVM Storage Flow
Disk → PV → VG → LV → Filesystem → Mount
3. Why lsblk and df -h Showed Different Sizes

After:

lvextend -L +200M /dev/devops-vg/app-data
lsblk showed updated LV size immediately
df -h still showed old filesystem size

Reason:

LV expanded
filesystem did not expand yet

Fixed using:

resize2fs /dev/devops-vg/app-data
4. Understanding Mount Points with and without LVM
Without LVM
Disk → Filesystem → Mount

Mount point appears directly on the disk in lsblk.

Example:

nvme4n1   /mnt/disk-mounts
With LVM
Disk → PV → VG → LV → Filesystem → Mount

Mount point appears on the LV instead of the raw disk.

Example:

my--vg-app--data   /mnt/app-data
Challenges Faced ⚠️
Challenge 1

mkfs.ext4 /dev/nvme1n1 failed with:

device is apparently in use by the system
Reason

The disk was already being used as a PV inside LVM.

Solution

Filesystem should be created on the LV, not directly on the PV disk.

Correct command:

mkfs.ext4 /dev/devops-vg/app-data
Challenge 2

lsblk showed increased size after lvextend
but df -h still showed old size.

Reason

Filesystem was not resized.

Solution
resize2fs /dev/devops-vg/app-data
