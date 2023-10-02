## Shell
### What is a shell?

**A shell is a program that provides an interface between a user and an operating system (OS) kernel.**
### Basic Architecture of the Shell

<img src="https://elearn.epam.com/assets/courseware/v1/1696ac3238ac82d1879ccc65d211fffc/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/shell_architecture.png" width="600" height="200" >

The fundamental architecture on which the hypothetical Shell is based isn’t complex. The basic architecture is pretty similar to a pipeline, where input is analyzed and parsed, symbols are expanded. It uses a variety of methods such as brace, tilde, variable and parameter expansion and substitution, and filename generation. Then, commands are executed using shell built-in commands, or external commands.

### Types

- The Bourne Shell (sh)
- The C Shell (csh)
- The Korn Shell (ksh)
- The GNU Bourne-Again Shell (bash)

### Comparison
| № | Shell | Path | Default Prompt(non-root user) | Default Prompt(root user) |
| :---: | :---: | :---: | :---: | :---: |
| 1 | **The Bourne Shell (sh)** | /bin/sh and /sbin/sh | $ | # |
| 2 | **The C Shell (csh)** | /bin/csh | % | # |
| 3 | **The Korn Shell (ksh)** | /bin/ksh | $ | # |
| 4 | **The GNU Bourne-Again Shell (Bash)** | /bin/bash | bash-x.xx$ | bash-x.xx# |

### Additional materials

[Difference Between Bash, Zsh, and Other Linux Shells](https://www.howtogeek.com/68563/htg-explains-what-are-the-differences-between-linux-shells/)
