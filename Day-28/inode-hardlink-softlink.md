### ⭐ What is inode?
An inode is a data structure in Linux that stores information about a file.

It stores → file owner, permissions, size, type, creation/modification time, location.
> **# No file name**

### ⭐ Why does Linux use inode?
Linux uses inode to separate the file name from file data, which makes file management faster & allows multiple names (hard link) for the same file just with two different names.

### ⭐ How to check inode no.?
```bash
ls -i FILE_NAME
```

### ⭐ Command to display inode
```bash
ls -i
```
### ⭐ What happens if two files have the same inode?
It means they are hard links to the same file. Both point to the same data.

### ⭐ What is hard link?
A hard link is another file name that points to the same inode.

### ⭐ What is softlink?
A soft link is a shortcut to another file. It points to file path, not inode.

### ⭐ Why hard link?
A hard link is used when we want multiple filenames for the same file without creating another copy. This saves disk space & ensures the file remains available even if one filename is deleted.

### ⭐ Why softlink?
It is like a shortcut. We use softlink as shortcuts to files or directories. They make it easier to access files from different locations & can link across file systems. If the original file is deleted, the softlink is broken.
