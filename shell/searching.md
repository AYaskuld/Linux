## Filesystem files search

- **find** - look for files and directories with given criterias

find [-H] [-L] [-P] [-D debugopts] [-Olevel] [path...] [expression]

$ find / -name hosts
$ find /home -user user

### Equal commands below:
$ find /tmp -name core -type f -exec rm {} \;  
$ find /tmp -name core -type f -print | xargs /bin/rm -  

find command has a lot of useful options. Please use man find to get acquainted with all of them.  

- **locate** file in filesystem  

locate – find files and directories with given name  

$ locate passwd  
/etc/passwd  

Note: locate uses its own database for search, results may not be actual for new files till database is updated. Because of that you should use updatedb before locate.   

/var/lib/mlocate/mlocate.db - The database searched by default  

- **grep**  

grep – print lines matching a pattern  

F.i. if you need to find files in HOME directory that contain a word "fun", you could use the next command:  

$ grep -r "fun" ~  
/home/vagrant/.bash_profile:# Get the aliases and functions  
/home/vagrant/.bashrc:# User specific aliases and functions  

Note: grep is a very powerful and customizable command with a lot of opportunities, such as using of regular expressions.
