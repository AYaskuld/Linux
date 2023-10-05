## Crond

**cron** - daemon to execute scheduled commands

   cron [-n | -p | -s | -m]  
   cron -x [ext,sch,proc,pars,load,misc,test,bit]

Cron should be started from /etc/rc.d/init.d or /etc/init.d

Cron searches **/var/spool/cron** for crontab files which are named after accounts in /etc/passwd; The founded crontabs are loaded into memory. Cron also searches for /etc/anacrontab and the files in the /etc/cron.d directory, which are in a different format. Cron examines all stored crontabs, checking each command to see if it should be run in the current minute. When executing commands, any output is mailed to the owner of the crontab (or to the user named in the MAILTO environment variable in the crontab, if such exists). Job output can also be sent to syslog by using the -s option.

**Crontab syntax**
<img src ="https://elearn.epam.com/assets/courseware/v1/a4672a4974432b7f66492bc94d8d575a/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/cron-script.png">

### EDIT

To add or update job in crontab, use below command. It will open crontab file in the editor where a job can be added/updated.

crontab -e

By default, it will edit crontab entries of current logged in user. To edit other user crontab use command as below

crontab -u username -e

Crontab (cron table) is a text file that specifies the schedule of cron jobs. There are two types of crontab files. The system-wide crontab files and individual user crontab files.

Users crontab files are stored by the user’s name, and their location varies by operating systems. In Red Hat based system such as CentOS, crontab files are stored in the /var/spool/cron directory while on Debian and Ubuntu files are stored in the **/var/spool/cron/crontabs** directory. Although you can edit the user crontab files manually, it is recommended to use the crontab command.

**/etc/crontab** and the files inside the **/etc/cron.d** directory are system-wide crontab files that can be edited only by the system administrators.

In most Linux distributions you can also put scripts inside the **/etc/cron.{hourly,daily,weekly,monthly}** directories and the scripts will be executed every hour/day/week/month.

### EXAMPLES

            Schedule a cron to execute at 2am daily
            0 2 * * * /bin/sh backup.sh
            Schedule a cron to execute twice a day
            0 5,17 * * * /scripts/script.sh
            Schedule a cron to execute on every minutes
            * * * * *  /scripts/script.sh
            Schedule a cron to execute on every Sunday at 5 PM
            0 17 * * sun  /scripts/script.sh
            Schedule a cron to execute on every 10 minutes
            */10 * * * * /scripts/monitor.sh
            Schedule a cron to execute on selected months
            * * * jan,may,aug *  /script/script.sh
            Schedule a cron to execute on selected days
            0 17 * * sun,fri  /script/script.sh
            Schedule a cron to execute on first sunday of every month
            0 2 * * sun  [ $(date +%d) -le 07 ] && /script/script.sh
            Schedule a cron to execute on every four hours
            0 */4 * * * /scripts/script.sh
            Schedule a cron to execute twice on every Sunday and Monday
            0 4,17 * * sun,mon /scripts/script.sh
            Schedule a cron to execute on every 30 Seconds
            * * * * *  sleep 30; /scripts/script.sh
            Schedule a multiple tasks in single cron
            * * * * * /scripts/script.sh; /scripts/scrit2.sh

### Online generator

Please take a look at online crontab generator by https://crontab.guru/
