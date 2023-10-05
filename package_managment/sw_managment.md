## Software Management

A software package refers to computer software packaged in an archive format to be installed by a package management system or a self-sufficient installer.

A package management system is a collection of tools to automate the process of installing, upgrading, configuring, and removing software packages from a computer.

Red Hat based:

- *.RPM
- rpm
- yum

Debian based:

- *.DEB
- pkg
- apt

**RPM** (Red Hat Package Manager) is a package management system. Originally developed by Red Hat for Red Hat Linux, RPM is now used by many Linux distributions.

**YUM** (The Yellow dog Updater, Modified) is an open source command line package management utility for RPM-compatible Linux operating systems and has been released under the GNU GPL.

deb is the extension of the Debian software package format and the most often used name for such binary packages. Like the "Deb" part of the term Debian, it originates from the name of Debra, then girlfriend and now ex-wife of Debian's founder Ian Murdock

**APT**, or The Advanced Packaging Tool, is a free user interface that works with core libraries to handle the installation and removal of software on the Debian GNU/Linux distribution and its variants.

### APT-GET

apt-get - is a simple command line interface for downloading and installing packages. The most frequently used commands are update and install.

- update - Retrieve new lists of packages
- upgrade - Perform an upgrade
- install - Install new packages (pkg is libc6 not libc6.deb)
- remove - Remove packages
- purge - Remove packages and config files
- check - Verify that there are no broken dependencies

apt-cache - is a low-level tool used to manipulate APT's binary cache files, and query information from them.

- showpkg - Show some general information for a single package
- search - Search the package list for a regex pattern
- show - Show a readable record for the package
- depends - Show raw dependency information for a package
```bahs
$ ls /etc/apt/sources.list /etc/apt/sources.list.d/
/etc/apt/sources.list

/etc/apt/sources.list.d/:
docker-ce.list      kubernetes.list        winehq.list
gns3.list           terraform.list         aws.list

$ cat /etc/apt/sources.list
deb http://ftp.by.debian.org/debian/ buster main non-free contrib
deb-src http://ftp.by.debian.org/debian/ buster main non-free contrib

deb http://security.debian.org/debian-security buster/updates main contrib non-free
deb-src http://security.debian.org/debian-security buster/updates main contrib non-free

# buster-updates, previously known as 'volatile'
deb http://ftp.by.debian.org/debian/ buster-updates main contrib non-free
deb-src http://ftp.by.debian.org/debian/ buster-updates main contrib non-free

deb http://deb.debian.org/debian buster-backports main contrib non-free
```
