## Introduction to Shells
### What is shell?

The UNIX shell program interprets user commands, which are either directly entered by the user, or which can be read from a file called the shell script or shell program.

Shell scripts are interpreted, not compiled.

The shell reads commands from the script line per line and searches for those commands on the system, while a compiler converts a program into machine readable form, an executable file - which may then be used in a shell script.

Apart from passing commands to the kernel, the main task of a shell is providing a user environment, which can be configured individually using shell resource configuration files.

The file /etc/shells gives an overview of known shells on a Linux system

To switch from one shell to another, just enter the name of the new shell in the active terminal.

localhost:~> tcsh

[localhost@post21 ~]$

### Shell types

- sh or Bourne Shell: the original shell still used on UNIX systems and in UNIX-related environments. This is the basic shell, a small program with few features. While this is not the standard shell, it is still available on every Linux system for compatibility with UNIX programs.
- bash or Bourne Again shell: the standard GNU shell, intuitive and flexible. Probably most advisable for beginning users while being at the same time a powerful tool for the advanced and professional user. On Linux, bash is the standard shell for common users. This shell is a so-called superset of the Bourne shell, a set of add-ons and plug-ins. This means that the Bourne Again shell is compatible with the Bourne shell: commands that work in sh, also work in bash. However, the reverse is not always the case.
- csh or C shell: the syntax of this shell resembles that of the C programming language. Sometimes asked for by programmers.
- tcsh or TENEX C shell: a superset of the common C shell, enhancing user-friendliness and speed. That is why some also call it the Turbo C shell.
- ksh or the Korn shell: sometimes appreciated by people with a UNIX background. A superset of the Bourne shell; with standard configuration a nightmare for beginning users.

### Shell auto-completion

Some shells like bash or zsh support auto-completion of entered commands or paths, f.i. you begin typing with cd /ro and then pressing on Tab key on a keyboard and entered path in command line is completed to full cd /root/

$ cd /ro       # now you press Tab here and get
$ cd /root/

If you press Tab one more time, shell will give you a hint with a list of files and directories inside /root/ folder

$ cd /root/       # now you press Tab here and get
$ cd /root/.      # . - dot character was added because all file/dir names start with it
./        ../       .bashrc   .docker/  .profile
$ cd /root/.b      # if you type b and press Tab again, you will get
$ cd /root/.bashrc

Auto-complition in Linux is also configurable, f.i. for Kubernetes CLI, more details by the link.
Bash startup files

Startup files are scripts that are read and executed by Bash when it starts. The following subsections describe different ways to start the shell, and the startup files that are read consequently.

**Invoked as an interactive login shell, or with `--login'**

Interactive means you can enter commands. The shell is not running because a script has been activated. A login shell means that you got the shell after authenticating to the system, usually by giving your user name and password.

Files read:

- /etc/profile
- ~/.bash_profile,
- ~/.bash_login or ~/.profile: first existing readable file is read
- ~/.bash_logout upon logout.

**Invoked as an interactive non-login shell**

A non-login shell means that you did not have to authenticate to the system. For instance, when you open a terminal using an icon, or a menu item, that is a non-login shell.

Files read:

- ~/.bashrc

This file is usually referred to in ~/.bash_profile
