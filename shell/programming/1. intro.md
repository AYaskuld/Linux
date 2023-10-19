## Shell Programming

SHELL is also a programming language:

- The syntax is simple and straightforward
- Most short scripts work right the first time
- Debugging is straightforward

The shell program interprets user commands, which are either directly entered by the user, or which can be read from a file called the shell script or shell program. Shell scripts are interpreted, not compiled. The shell reads commands from the script line per line and searches for those commands on the system, while a compiler converts a program into machine readable form, an executable file - which may then be used in a shell script.
Environment Variables and Shell Variables

In Linux and Unix based systems environment variables are a set of dynamic named values, stored within the system that are used by applications and shell scripts launched in shells or subshells. In simple words, an environment variable is a variable with a name and an associated value.

Environment variables allow you to customize how the system works and the behavior of the applications on the system or use values of environment variables inside of your shell scripts. For example, the environment variable can store information about the default text editor or browser, the path to executable files, or the system locale and keyboard layout settings.  

Note: Additional details of shell scripting you will learn during Bash scripting course later.

Variables have the following format:
```bash
KEY=value
ANOTHER_KEY="Some other value"
KEY_MULTI=value1:value2
```
- The names of the variables are case-sensitive. By convention, environment variables should have UPPER_CASE names with underscore _ character between words.
- When assigning multiple values to the variable they must be separated by the colon : character.
- There is no space around the equals = symbol.

Variables can be classified into two main categories, environment variables, and shell variables.

Environment variables are variables that are available system-wide and are inherited by all spawned child processes and shells.

Shell variables are variables that apply only to the current shell instance. Each shell such as zsh and bash, has its own set of internal shell variables.

Commands how to set environment and shell variables will be described in the next chapter.

Below are some of the most common environment variables:

- USER - The current logged in user.
- HOME - The home directory of the current user.
- EDITOR - The default file editor to be used. This is the editor that will be used when you type edit in your terminal.
- SHELL - The path of the current user’s shell, such as bash or zsh.
- LOGNAME - The name of the current user.
- PATH - A list of directories to be searched when executing commands.
 Note: When you run a command the system will search those directories in this order and use the first found executable.
- LANG - The current locales settings.
- TERM - The current terminal emulation.
- MAIL - Location of where the current user’s mail is stored.

### When not to use shell scripts

- Resource-intensive tasks, especially where speed is a factor (sorting, hashing, recursion)
- Complex applications, where structured programming is a necessity (type-checking of variables, function prototypes, etc.)
- Mission-critical applications upon which you are betting the future of the company
- Situations where security is important, where you need to guarantee the integrity of your system and protect against intrusion, cracking, and vandalism
- Need native support for multi-dimensional arrays
- Need data structures, such as linked lists or trees
- Need to generate / manipulate graphics or GUIs
- Need to use libraries or interface with legacy code
- Proprietary, closed-source applications (Shell scripts put the source code right out in the open for all the world to see.)

