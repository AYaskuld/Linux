## Systemd/init.d

### init.d

The init.d directory contains a number of start/stop scripts for various services on your system.

/etc/init.d/command OPTION

Where command is the actual command to run and OPTION can be one of the following:

- start
- stop
- reload
- restart
- force-reload
```bash
# cat /etc/init.d/static_routes
#!/sbin/sh 
# Add static routes
GW=10.204.223.1
case "$1" in 'start’)       
  /usr/sbin/route add -net 10.204.0.0   -netmask 255.255.0.0   $GW        
  /usr/sbin/route add -net 10.200.0.0   -netmask 255.255.0.0   $GW        
  exit 0        
;;'stop’)        
   exit 0        
;; *)        
   echo "Usage: $0 { start | stop }"        
   exit 1        
;; 
esac
```
### Systemd

**systemd** is a system and service manager for Linux operating systems. When run as a system instance, systemd interprets the configuration file system.conf and the files in system.conf.d directories; when run as a user instance, systemd interprets the configuration file user.conf and the files in user.conf.d directories.

**systemd** is not just the name of the init daemon but also refers to the entire software bundle around it, which, in addition to the systemd init daemon, **includes** the daemons **journald, logind and networkd**, and many other low-level components.

Systemd “.target” encodes information about a target unit of systemd, which is used for grouping units and as well-known synchronization points during start-up. Target units are a more flexible replacement for SysV (init.d) runlevels in the classic SysV init system. (For compatibility reasons special target units such as runlevel3.target exist which are used by the SysV runlevel compatibility code in system)

<img src ="https://elearn.epam.com/assets/courseware/v1/c53446c5396234b5e982c0f62aebb20e/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/targets.png">

**systemd** records initialization instructions for each daemon in a configuration file (referred to as a "unit file") that uses a declarative language, replacing the traditionally used per-daemon startup shell scripts.

**/usr/lib/systemd/system/** – unit files for rpm based packages, like nginx, apacheг, mysql and others/run/systemd/system/ — unit files created at runtime/etc/systemd/system/  — user created unit files

Unit file types include service, socket, device, mount, automount, swap, target, path, timer (which can be used as a cron-like job scheduler), snapshot, slice and scope.

Unit file syntax is .ini file like. Each unit file consist of 3 sections: [Unit], [Service] and [Install]

The [**Unit**] section contains generic information about the service. systemd not only manages system services, but also devices, mount points, timer, and other components of the system. The generic term for all these objects in systemd is a unit, and the [Unit] section encodes information about it that might be applicable not only to services but also in to the other unit types systemd maintains.

**Description** = A descriptive information along with the unit name 

**Documentation** = A list of man pages referencing for this unit or its configuration 

**Requires**= According to man page, this configures requirement dependencies on other units. If this unit gets activated, the units listed here will be activated as well. If one of the other units gets deactivated or its activation fails, this unit will be deactivated. Note that requirement dependencies do not influence the order in which services are started or stopped. This has to be configured independently with the After= or Before= options. 

**Wants**= A weaker version of Requires=. A unit listed in this option will be started if the configuring unit is. However, if the listed unit fails to start up or cannot be added to the transaction this has no impact on the validity of the transaction as a whole. 

**Conflicts**= Configures negative requirement dependencies. If a unit has a Conflicts setting on another unit, starting the former will stop the latter and vice versa.  

**Before**= Configures ordering dependencies between units. If a unit foo.service contains a setting “Before=bar.service” and both units are being started, bar.service's start-up is delayed until foo.service is started up.  

**After**= It is the inverse of “Before=”  

**AllowIsolate**= If true this unit may be used with the “systemctl isolate” command. Otherwise this will be refused.  

**ConditionPathExists**= a file existence condition is checked before a unit is started. If the specified absolute path name does not exist the condition will fail  

**ConditionPathIsDirectory**= is similar to ConditionPathExists but verifies whether a certain path exists and is a directory

The next section is [**Service**] which encodes information about the service itself. It contains all those settings that apply only to services, and not the other kinds of units systemd maintains (mount points, devices, timers, ...).

**Type**= Configures the process start-up type for this service unit. One ofsimple,exec,forking,oneshot,dbus,notify or idle**

**PIDFile**= Takes a path referring to the PID file of the service. Usage of this option is recommended for services where **Type**= is set to forking.

**ExecStart**= Commands with their arguments that are executed when this service is started. The value is split into zero or more command lines according to the rules described below (see section "Command Lines" below). Unless Type= is oneshot, exactly one command must be given. When Type=oneshot is used, zero or more commands may be specified.

**ExecStartPre**=, **ExecStartPost**= Additional commands that are executed before or after the command in ExecStart=, respectively.

**ExecReload**= Commands to execute to trigger a configuration reload in the service.

**ExecStop**= Commands to execute to stop the service started via ExecStart=.

**Restart**= Configures whether the service shall be restarted when the service process exits, is killed, or a timeout is reached.

The final section is [**Install**]. It encodes information about how the suggested installation should look like, i.e. under which circumstances and by which triggers the service shall be started.

**Alias**= Additional names this unit shall be installed under. The names listed here must have the same suffix (i.e. type) as the unit file name.

**Also**= Additional units to install/deinstall when this unit is installed/deinstalled

**WantedBy**=, RequiredBy= This option creates a symbolic link to the unit in a “.wants” subdirectory for the WantedBy unit.

**WorkingDirectory**= Takes an absolute directory path. Sets the working directory for executed processes.

**RootDirectory**= Takes an absolute directory path. Sets the root directory for executed processes, with the chroot system call.

**User**=, **Group**= Sets the Unix user or group that the processes are executed as, respectively.

**Nice**= Sets the default nice level (scheduling priority) for executed processes.

**CPUSchedulingPriority**= Sets the CPU scheduling priority for executed processes.

**UMask**= Controls the file mode creation mask. Default is 022.

**Environment**= Sets environment variables for executed processes. Takes a space-separated list of variable assignments.  

**EnvironmentFile**= Similar to Environment= but reads the environment variables from a text file. The text file should contain new-line separated variable assignments. Empty lines and lines starting with ; or # will be ignored, which may be used for commenting.

**StandardOutput**= Set output to a log, console, or null.

**SyslogFacility**= Sets the syslog facility to use when logging to syslog. One of kern, user, mail, daemon, auth, syslog, lpr, news, uucp, cron, authpriv, ftp, local0, local1, local2, local3, local4, local5, local6 or local7.  

**SyslogLevel**= Default syslog level to use when logging to syslog or the kernel log buffer. One of emerg, alert, crit, err, warning, notice, info, debug.

**MemoryLimit**= Limit the overall memory usage of the executed processes to a certain size.

**DeviceAllow**=, DeviceDeny= Control access to specific device nodes by the executed processes.
```bash
$ cat /etc/systemd/system/tomcat.service
[Unit]
Description=Tomcat Application server
After=network.target

[Service]
Type=forking
ExecStart=/apps/tomcat/bin/startup.sh
ExecStop=/apps/tomcat/bin/shutdown.sh
User=tomcat55
Group=staff

[Install]
WantedBy=multi-user.target
```
```bash
# systemctl start [name.service]
# systemctl stop [name.service]
# systemctl restart [name.service]
# systemctl reload [name.service]
# systemctl status [name.service]
# systemctl is-active [name.service]
# systemctl list-units --type service --all
```
