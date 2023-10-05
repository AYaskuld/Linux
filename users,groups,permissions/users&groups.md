## Users and Groups

Each user in UNIX has the following parameters:

- User name
- Encrypted password (or 'x' if hash is stored)
- User Identifier (UID)
- Group Identifier (GID)
- Full name or description
- User’s home directory
- User’s shell
- Expiration date

Each group in UNIX has the following parameters:

- Group name
- Encrypted password (or 'x' if hash is stored)
- Group Identifier (GID)

List of usernames for people who are members of this group By default in any UNIX created some users.Information about all users you can find in file **/etc/passwd**.
```bash
$ cat /etc/passwd
root:x:0:1:Super-User:/:/sbin/sh 
daemon:x:1:1::/: 
bin:x:2:2::/usr/bin: 
sys:x:3:3::/: 
adm:x:4:4:Admin:/var/adm: 
lp:x:71:8:Line Printer Admin:/usr/spool/lp: 
uucp:x:5:5:uucp Admin:/usr/lib/uucp: 
nuucp:x:9:9:uucp Admin:/var/spool/uucppublic:/usr/lib/uucp/uucico smmsp:x:25:25:SendMail Message Submission Program:/: 
listen:x:37:4:Network Admin:/usr/net/nls: 
nobody:x:60001:60001:Nobody:/: 
```
User parameters:

<img src = "https://elearn.epam.com/assets/courseware/v1/deaa3c2064808cf7ba901c068d4a2ec8/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/user-param.png">

Each user should belong to User group (at least one). Information about these groups you can find in file **/etc/group**.
```bash
$ cat /etc/group
root::0:root 
other::1: 
bin::2:root,bin,daemon 
sys::3:root,bin,sys,adm 
adm::4:root,adm,daemon 
uucp::5:root,uucp 
mail::6:root 
tty::7:root,adm 
lp::8:root,lp,adm 
nuucp::9:root,nuucp 
staff::10:
```

Group parameters:
<img src="https://elearn.epam.com/assets/courseware/v1/8fdf076d28891fcd3b3c0604697b6a4b/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/group-param.png">

**root is super user. It has unlimited rights in the system.**

**Do not use without necessity!**

User:

- su
- sudo
- useradd
- userdel
- usermod
- passwd
- finger

Groups:

- groupadd
- groupdel
- groupmod
- groups

### Substitute User

**su** - switch between users

Note: you should know password of user to which you want switch
```bash
# su - user or su user
# su
# su root
```

**Super user do**

**sudo** - run programs with the security privileges of another user.

Note: Prompts for a current user password by default
```bahs
# sudo ifconfig
# sudo su ---- the same as su but doesn’t require root password
```
**Add user**

**useradd** - create user (requires root access)
```bash
# useradd –d /home/mydir –s /bin/bash user1
```
<img src="https://elearn.epam.com/assets/courseware/v1/0f860fc356f7ce6508c7c126ae65c580/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/useradd.png">

**Delete user**

**userdel** - delete user (requires root access)
```bahs
# userdel user - Delete user user
# userdel –r tester - Delete user tester with its home directory and files
```

**Modify user settings**

**usermod** - modify user account information (requires root access)
```bash
# usermod -d /home/newhome user - modify the home directory for the user account to "/home/newhome"
```
**Change password**

**passwd** - change of user password
```bash
#passwd - command
april09 - current password
finalday - new password
finalday
```

**How to get user info**

**finger** - get user detailed info
```bash
# finger user
Login name: user
Directory: /home/myfolder 
Shell: /bin/bash
```
**How to add a user group**

**groupadd** – create a new group

```bash
# groupadd mytestgroup - Create group “mytestgroup”
```
