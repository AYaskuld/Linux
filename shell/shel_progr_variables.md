## Variables

Variables are how programming and scripting languages represent data. A variable is nothing more than a label, a name assigned to a location or set of locations in computer memory holding an item of data.

**Assignment**:
```bash
var=value
var2="one two three"
var3=one\ two\ three
```
**Referencing a variable**:
```bash
echo $var
echo ${var}
```
**Indirect referencing:**
```bash
var=value
value=hello
eval b=\$$var
echo $b
```
### Variable Types

Bash does not segregate its variables by "type."

Essentially, Bash variables are character strings, but, depending on context, Bash permits arithmetic operations and comparisons on variables. The determining factor is whether the value of a variable contains only digits.

The declare or typeset built-ins, which are exact synonyms, permit modifying the properties of variables.
```bash
$ n=6/3
$ echo "n = $n"
n = 6/3

$ declare -i n
$ n=6/3
$ echo "n = $n"
n = 2
```
### Manipulating Strings

Bash supports a surprising number of string manipulation operations:

- **${#var}** - **$var** length. For an array, ${#array} is the length of the first element in the array.
```bash
$ stringZ=abcABC123ABCabc
$ echo ${#stringZ}
15

$ arrayX=(a ab abc)
$ echo ${#arrayX}
1
```
- **${var:position:length}** - extracts $length characters of substring from $var at $position. 0-based indexing.
```bash
$ stringZ=abcABC123ABCabc
$ echo ${stringZ:2:5}
cABC1
```
- **${var#Pattern}** - remove from $var the shortest part of $pattern that matches the front end of $var.

- **${var##Pattern}** - remove from $var the longest part of $pattern that matches the front end of $var.
```bash
$ stringZ=abcABC123ABCabc
$ echo ${stringZ#a*C}
123ABCabc
$ echo ${stringZ##a*C}
abc
```
- **${var%Pattern}** - deletes shortest match of $Pattern from back of $var.

- **${var%%Pattern}** - deletes longest match of $Pattern from back of $string.
```bash
$ stringZ=abcABC123ABCabc
$ echo ${stringZ%a*c}
abcABC123ABC
$ echo ${stringZ%%b*c}
a
```
- **${var/Pattern/Replacement}** - replace first match of $Pattern with $Replacement. If $Replacement is omitted, then the first match of $Pattern is replaced by nothing, that is, deleted.

- **${var//Pattern/Replacement}** - replace all matches of $Pattern with $Replacement.
```bash
$ stringZ=abcABC123ABCabc
$ echo ${stringZ/abc/xyz}
xyzABC123ABCabc
$ echo ${stringZ//abc/xyz}
xyzABC123ABCxyz
$ stringZ=abcABC123ABCabc
$ echo ${stringZ/abc}
ABC123ABCabc
$ echo ${stringZ//abc}
ABC123ABC
```
- **${var/#Pattern/Replacement}** - if prefix of $var matches $Pattern, then substitute $Replacement for $Pattern.

- **${var/%Pattern/Replacement}** - if suffix of $var matches $Pattern, then substitute $Replacement for $Pattern.
```bash
$ stringZ=abcABC123ABCabc
$ echo ${stringZ/#abc/XYZ}
XYZABC123ABCabc
$ echo ${stringZ/%abc/XYZ}
abcABC123ABCXYZ
```
### Parameter substitution

- **${parameter-default}, ${parameter:-default}** - if $parameter not set, use default. ${parameter-default} and ${parameter:-default} are almost equivalent. The extra ":" makes a difference only when $parameter has been declared, but is null.
```bash
$ var1=1
$ var2=2
$ echo ${var1-$var2}
1
$ echo ${var3-$var2}
2
$ var1=1
$ var3=           # declared but null
$ echo ${var3-$var1}
$ echo ${var3:-$var1}
1
```
The default parameter construct finds use in providing "missing" command-line arguments in scripts.
```bash
#!/bin/bash

DEFAULT_FILENAME=generic.data

# If not otherwise specified, the following command block operates on the
# file "generic.data".

filename=${1:-$DEFAULT_FILENAME}
...
```

- **${parameter=default}, ${parameter:=default}** - if $parameter not set, set it to $default. Both forms nearly equivalent. The ":" makes a difference only when $parameter has been declared and is null.
```bash
$ varZ= 
$ echo ${varZ=abc}
$ echo ${varZ:=abc}
abc
$ echo ${var=abc}
abc
$ echo ${var=xyz}
abc
```
- **${parameter+alt_value}, ${parameter:+alt_value}** - if $parameter set, use $alt_value, else use null string. Both forms nearly equivalent. The ":" makes a difference only when $parameter has been declared and is null.
```bash
$ a=${param1+xyz}
$ echo "a = $a"
a =
$ param2=
$ a=${param2:+xyz}
$ echo "a = $a"
a = xyz
```
- **${parameter?err_msg}, ${parameter:?err_msg}** if $parameter set, use it, else print $err_msg and abort the script with an exit status of 1. Both forms nearly equivalent. The ":" makes a difference only when parameter has been declared and is null.
```bash
#!/bin/bash

: ${HOSTNAME?} ${USER?} ${MAIL?}
echo "Name of the machine is $HOSTNAME."
echo "You are $USER."
echo "Your mail INBOX is located in $MAIL."
echo
echo "If you are reading this message,"
echo "critical environmental variables have been set."
echo
```
### Special variables types

- Local variables
- Environment variables
- Positional parameters
- Built-in variables

**Local variables**

Variables visible only within a code block or function.
```bash
$ func() {
  local var=$1
  echo $var
}

$ echo $var
$ func Hello
Hello
```
**Environment variables**

Variables that affect the behavior of the shell and user interface.

Environment variables can be set:
- system-wide:
    - /etc/environment  
- for current session:
    - export MYVAR=value  
- for all sessions of a user
    - ~/.bashrc  
    - ~/.bash_profile  
- during script execution:
```bash
#!/bin/bash

. ~/my_env_vars # or: source ~/my_env_vars
```
How to check current environment variables?
```bash
$ env
LC_ADDRESS=en_US.UTF-8
HOSTNAME=node1
LC_MONETARY=en_US.UTF-8
TERM=xterm-256color
SHELL=/bin/bash
HISTSIZE=1000
SSH_CLIENT=10.0.2.2 37896 22
LC_NUMERIC=en_US.UTF-8
SSH_TTY=/dev/pts/0
USER=vagrant
...
```
### Positional parameters

Arguments passed to the script from the command line: $0, $1, $2, $3 . . .  

$0 is the name of the script itself, $1 is the first argument, $2 the second, $3 the third, and so forth.  

After $9, the arguments must be enclosed in brackets, for example, ${10}, ${11}, ${12}.  

$# number of command-line arguments or positional parameters.  

The special variables "$*" and "$@" denote all the positional parameters.  
```bash
#!/bin/bash

NUMBER=1

for arg in $@; do
  echo -e "argument #${NUMBER}: $arg";
  ((NUMBER++));
done
```
```bash
$ bash script.sh 1 apple hello 4
argument #1: 1
argument #2: apple
argument #3: hello
argument #4: 4
```
### Built-in variables
![изображение](https://github.com/AYaskuld/Linux/assets/98359811/4d723418-b523-49cf-976b-c711c57dfb92)

### Special shell variables
![изображение](https://github.com/AYaskuld/Linux/assets/98359811/a569106d-5b02-44ea-aa9c-26dc193f5045)

### Arrays

An array is a variable containing multiple values. Any variable may be used as an array. There is no maximum limit to the size of an array, nor any requirement that member variables be indexed or assigned contiguously. 

Arrays are zero-based: the first element is indexed with the number 0.
```bash
$ my_array=( zero one two three four five 
```
Array elements may be initialized with the following notation:
```bash
$ my_array[6]=six
```
Alternatively, a script may introduce the entire array by an explicit statement:
```bash
$ declare -a new_array
```
To dereference (retrieve the contents of) an array element, use curly bracket notation:
```bash
$ echo ${my_array[6]}
six
```
Refer all array elements:
```bash
$ my_array=( zero one two three four five )
$ echo ${my_array[@]}
zero one two three four five six
$ echo ${my_array[*]}
zero one two three four five six
```
Get the the number of elements in array:
```bash
$ echo ${#my_array[@]}
7
$ echo ${#my_array[*]}
7
```
