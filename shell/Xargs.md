## Xargs

xargs - reads arguments from the standard input, separated by blank spaces or newlines, and executes the specified command using the input as command’s arguments. If no command is provided, default is /bin/echo. 

The syntax for the xargs command is as follows:

xargs [OPTIONS] [COMMAND [initial-arguments]]

$ cat names.txt  
one   
two  
three  

### from multiline to a single line
$ cat names.txt | xargs  
one two three  

$ cat names.txt | xargs -i touch {}  
$ ls  
names.txt  one  three  two  

### or equivalent of the previous command
$ cat names.txt | xargs -iT touch T  

-0, --null

Input items  are  terminated  by a null character instead of by whitespace, and the quotes and backslash are not special (every character is taken literally). Useful when input items might contain white space, quote marks, or backslashes.

-P max-procs, --max-procs=max-procs

Run up to max-procs processes at a time; the default is 1.  This speeds up execution in a machine with a multicore CPU. If max-procs is 0, xargs will run as many processes as possible at a time.

Please look through examples of usage and addtitional options:

- https://www.tecmint.com/xargs-command-examples/
- https://linuxize.com/post/linux-xargs-command/

