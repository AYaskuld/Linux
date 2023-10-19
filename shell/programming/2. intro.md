## Script Development and Invocation

In the simplest case, a script is nothing more than a list of system commands stored in a file. At the very least, this saves the effort of retyping that particular sequence of commands each time it is invoked.  

**The sha-bang ( #!)** at the head of a script tells your system that this file is a set of commands to be fed to the command interpreter indicated. Immediately following the sha-bang is a path name. This is the path to the program that interprets the commands in the script, whether it be a shell, a programming language, or a utility.

- #!/bin/sh
- #!/bin/bash
- #!/usr/bin/perl
- #!/usr/bin/env python
- #!/bin/sed -f
- #!/bin/awk -f

Having written the script, you can invoke it by sh scriptname, or alternatively bash scriptname. 

Much more convenient is to make the script itself directly executable with a chmod and run it by ./scriptname.

## Bash Options

Options are settings that change shell and/or script behavior.  

The **set** command enables options within a script. At the point in the script where you want the options to take effect, use **set -o option-name** or, in short form, **set -option-abbrev**. These two forms are equivalent:

- set -o verbose
- set -v

To disable an option within a script, use set +o option-name or set +option-abbrev.

- set +o verbose
- set +v
  
![изображение](https://github.com/AYaskuld/Linux/assets/98359811/fa741c27-b12a-49e8-859e-5049e67e5d6f)

Example 1:
```bash
#!/bin/bash

# exit_on_error.sh
set -e

echo "Check non-existing file"
cat non-existing-file.txt 
echo "moving on"

$ ./exit_on_error.sh 
Check non-existing file
cat: non-existing-file.txt: No such file or directory
```
Example 2:
```bash
#!/bin/bash

# skip_error.sh
# default value is +e

echo "Check non-existing file"
cat non-existing-file.txt 
echo "moving on"

$ ./skip_error.sh 
Check non-existing file
cat: non-existing-file.txt: No such file or directory
moving on
```
## Exit Codes

![изображение](https://github.com/AYaskuld/Linux/assets/98359811/28483727-4cba-498e-a828-907d28de3330)

## Special Characters

What makes a character special?

If it has a meaning beyond its literal meaning, a meta-meaning, then we refer to it as a special character. Along with commands and keywords, special characters are building blocks of Bash scripts. 

![изображение](https://github.com/AYaskuld/Linux/assets/98359811/040abb1c-ec41-4921-a9f2-241a8bb924d8)


