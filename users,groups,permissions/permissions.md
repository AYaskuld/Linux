## Permission model

Files and devices may be granted access based on a users ID or group ID (owner and group owner)
```bash
# ls -l
```
<img src = "https://elearn.epam.com/assets/courseware/v1/72e4e473929afbc1b279bff22665a4a3/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/file-perm.png">

### Change directory’s user owner

**chown** - make user directory’s owner
```bash
# chown user /home/myfolder - Make user the owner of “/home/myfolder” directory
```
### Change directory’s group owner

**chgrp** - make an owner group for file
```bash
# chgrp mytestgroup test.t - Make ‘mytestgroup’ group the owner group for ‘test.t’ file
```
### Access permissions

File, directory and device (special file) permissions are granted based on user, group or other (world) identification status. Permission is granted (or denied) for read (r), write (w) and execute (x) access.
Access permissions: octal numerical representation

r = 4  
w = 2   
x = 1  

Example:

converting rwxr-x--- to octal, for that we need to devide in 3 groups with 3 characters in each rwx, r-x, --- and then convert each of them:  
7 = 4+2+1 = r + w + x  
5 = 4+1 = r + x (no write)  
0 = --- = no rights  
So rwxr-x--- is 750 in octal.  

### Change access mode  

**chmod** – change permissions for file
```bash
# chmod g=rw test.t - Give read and write rights to group for ‘test.t’ file
# chmod 755 test.t - Give rwxr-xr-x permission for test.t using octal form
# chmod o-r,g+w test.t
```
### Sticky bit

The sticky bit is primarily used on shared directories.  
It is useful for shared directories such as /var/tmp and /tmp because users can create files, read and execute files owned by other users, but are not allowed to remove files owned by other users.  
For example if user bob creates a file named /tmp/bob, other user tom can not delete this file even when the /tmp directory has permission of 777. If sticky bit is not set then tom can delete /tmp/bob, as the /tmp/bob file inherits the parent directory permissions.  
```bash
# chmod +t somedirectory - where 1 = sticky bit
# chmod 1700 somedirectory
# chmod -t somefile - - where the zero would mean no sticky bit
# chmod 0700 somefile
```
### SUID\SGID

Set-user Identification (SUID) and Set-group identification (SGID)

- The setuid permission displayed as an “s” in the owner’s execute field.
- When a command or script with SUID bit set is run, its effective UID becomes that of the owner of the file, rather than of the user who is running it.
- to set SUID on a file
```bash
# chmod 4555 [path_to_file]
```
The setgid permission displays as an “s” in the group’s execute field.

- SGID permission is similar to the SUID permission, only difference is – when the script or command with SGID on is run, it runs as if it were a member of the same group in which the file is a member.
- to set SGID on a folder
```bash
# chmod 2555 [path_to_folder]
```
### lsattr

This will list if whether a file has any special attributes (as set by chattr). Use the -R option to list recursively and try using the -d option to list directories like other files rather than listing their contents. Command syntax:
```bash
# lsattr
```
This will list files in the current directory, you may also like to specify a directory or a file:
```bash
# lsattr /directory/or/file 
```
### chattr

Change file system attributes

- i: sets the 'immutable' flag on a file - will prevent any changes (accidental or otherwise) to the “lilo.conf” file. If you wish to modify the lilo.conf file you will need to unset the immutable flag: chattr -i.
```bash
# chattr +i /sbin/lilo.conf
```
- A: sets no Access time flag - if a file or directory has this attribute set, whenever it is accessed, either for reading of for writing, it's last access time will not be updated. This can be useful, for example, on files or directories which are very often accessed for reading, especially since this parameter is the only one which changes on an inode when it's opened.
- a: sets append only flag - if a file has this attribute set and is open for writing, the only operation possible will be to append data to it's previous contents. For a directory, this means that you can only add files to it, but not rename or delete any existing file.
- s: sets secure deletion flag - when such a file or directory with this attribute set is deleted, the blocks it was occupying on disk are written back with zeroes (similar to using shred).

Please come across additional examples and explanation by the [link](https://wiki.archlinux.org/title/File_permissions_and_attributes).
