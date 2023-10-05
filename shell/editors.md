## Text Editors

Text editors are one of the most frequently used applications on Unix systems. They are used to create and edit files in plain text format.

Currently the most popular text editors are:

- vi/vim
- nano

Default editor can be set via EDITOR environment variable.

### VI/VIM :

The original vi (visual editor) was developed by Bill Joy in 1976 as part of BSD Unix system. Bill Joy was later one of the co-founders of Sun Microsystems. vi became popular very fast within the Unix community as it provided a full screen, visual editor, which was missing before. It is still the standard text editor that is available on any Unix system.

Vim stands for Vi IMproved. It used to be Vi IMitation, but there are so many improvements that a name change was appropriate. Vim is a text editor which includes almost all the commands from the Unix program "Vi" and a lot of new ones

To start editing file simply run:
```bash
$ vim file_to_edit.txt
```
Learn VIM:
```bash
$ vimtutor
```
https://www.linux.com/tutorials/vim-101-beginners-guide-vim/

https://vim-adventures.com/

### VIM modes

vim has three modes:

- Command mode
- Input mode
- Last-line mode

**VIM command mode**

When vim starts up, it is in Command Mode. This mode is where vim interprets any characters we type as commands and thus does not display them in the window. In Command Mode, one can move around on the screen, search the document for words or phrases, delete portions of text and move text around.

To enter into Command Mode from any other mode, it requires pressing the [Esc] key.

- navigation
<img src = "https://elearn.epam.com/assets/courseware/v1/7ee9b2e1ed0b9dc6eeca0dbf613609d6/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/vim_navigation.png">
- editing
  <img src ="https://elearn.epam.com/assets/courseware/v1/fa7550018dad2424337c322bc1ce49c5/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/vim_editing.png">
- searching
  <img src ="https://elearn.epam.com/assets/courseware/v1/93fc615da9674134ce6cd610fb9f3598/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/vim_seraching.png">

### VIM insert mode

This mode enables you to insert text into the file. Everything that’s typed in this mode is interpreted as input and finally, it is put in the file. The vi always starts in command mode. To enter text, you must be in Insert Mode. To come in insert mode you simply type i.

You can type normally until you want to make a correction, save the file, or perform another operation that’s reserved for Command Mode or Last-line Mode. To get out of Insert Mode, hit the [Esc] key

### VIM Last-Line Mode (Escape Mode)

Line Mode is invoked by typing a colon [:], while vim is in Command Mode. The cursor will jump to the last line of the screen and vim will wait for a command. This mode enables you to perform tasks such as saving files, executing commands.
<img src ="https://elearn.epam.com/assets/courseware/v1/878e9f1987627c9377aacd93a03014fc/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/vim_last_line_mode.png">
VI/VIM cheatsheet
<img src = "https://elearn.epam.com/assets/courseware/v1/a7671349f53596966531589b731e4302/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/vim_cheatsheet.png">

### NANO

nano is a small and friendly text editor. Besides basic text editing, nano offers features like undo/redo, syntax coloring, interactive search-and-replace, auto-indentation, line numbers, word completion, file locking, backup files, and internationalization support.

nano is a "modeless" editor. This means that all keystrokes, with the exception of Control and Meta sequences, enter text into the file being edited.

Usual way to invoke nano is:

$ nano file_to_edit.txt

- Commands are given by using the Control key (Ctrl, shown as ^) or the Meta key (Alt or Cmd, shown as M-)
- Text can be cut from a file, a whole line at a time, by using the Cut Text command (default key binding: ^K).
- The contents of the cutbuffer can be pasted back into the file with the Uncut Text command (default key binding: ^U)
- A line of text can be copied into the cutbuffer (without cutting it) with the Copy Text command (default key binding: M-6).

### VISUDO

visudo is a specialized command for safe edit of a file located at /etc/sudoers, the sudo command is configured through this file.

Warning:  Never edit this file with a normal text editor! Always use the visudo command instead!

Because improper syntax in the /etc/sudoers file can leave you with a broken system where it is impossible to obtain elevated privileges, it is important to use the visudo command to edit the file.

The visudo command opens a text editor like normal, but it validates the syntax of the file upon saving. This prevents configuration errors from blocking sudo operations, which may be your only way of obtaining root privileges.

Traditionally, visudo opens the /etc/sudoers file with the vi text editor. Ubuntu, however, has configured visudo to use the nano text editor instead.

Additional details about visudo and sudo configuration are available [here](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file).
