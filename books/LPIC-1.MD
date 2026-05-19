# LPIC 1

- [LPIC 1](#lpic-1)
  - [useful tips](#useful-tips)
  - [vim Editor](#vim-editor)
    - [Command Mode](#command-mode)
    - [Insert Mode](#insert-mode)
    - [Ex Mode](#ex-mode)
    - [vim TIPS](#vim-tips)
  - [101 System Architecture](#101-system-architecture)
    - [101.1 Determine and configure hardware settings](#1011-determine-and-configure-hardware-settings)
    - [101.2 Boot the System](#1012-boot-the-system)
    - [101.3 Change runlevels/boot targets and shutdown or reboot system](#1013-change-runlevelsboot-targets-and-shutdown-or-reboot-system)
  - [102 Linux Installation and Package Management](#102-linux-installation-and-package-management)
    - [102.1 Design hard disk layout](#1021-design-hard-disk-layout)
    - [102.2 Install a boot manager](#1022-install-a-boot-manager)
    - [102.3 Manage shared libraries](#1023-manage-shared-libraries)
    - [102.4 Use Debian package management](#1024-use-debian-package-management)
    - [102.5 Use RPM and YUM package management](#1025-use-rpm-and-yum-package-management)
    - [102.6 Linux as a virtualization guest](#1026-linux-as-a-virtualization-guest)
  - [103 GNU and Unix Commands](#103-gnu-and-unix-commands)
  - [104 Devices, Linux Filesystems, Filesystem Hierarchy Standard](#104-devices-linux-filesystems-filesystem-hierarchy-standard)
    - [104.1 Create partitions and filesystems](#1041-create-partitions-and-filesystems)
    - [104.2 Maintain the integrity of filesystems](#1042-maintain-the-integrity-of-filesystems)
    - [104.3 Control mounting and unmounting of filesystems](#1043-control-mounting-and-unmounting-of-filesystems)
    - [103.4 Removed](#1034-removed)
    - [104.5 Manage file permissions and ownership](#1045-manage-file-permissions-and-ownership)
    - [104.6 Create and change hard and symbolic links](#1046-create-and-change-hard-and-symbolic-links)
    - [104.7 Find system files and place files in the correct location](#1047-find-system-files-and-place-files-in-the-correct-location)


## useful tips
| Terminal Shortcuts | Description |
|---|---|
| CTRL + C | Kill command |
| CTRL + L | Clear screen |
| CTRL + A | Start of line |
| CTRL + E | End of line |
| !! | Previous command |
| !git | Last command starting with git |

<br>
<br>

| Command / Path | Description | Note |
|---|---|---|
| `/tmp` | Temporary files | |
| `/etc` | System configs | |
| `pwd` | shows current directory | |
| `cd -` | jumps to previous directory. | |
| `mkdir myproject` | create folder | |
| `mkdir -p project/new/v1` | create nested folder | |
| `touch main.go` | create file | |
| `cat file.txt` OR `batcat file.txt` | view file | |
| `vim file.txt `| edit file | i → insert mode <br> ESC → command mode <br> :wq → save and quit <br> :q! → quit without save |
| `xdg-open file.pdf` | open PDF files | |
| `rm file.txt` | remove file | |
| `rm -r project` | delete folder recursively | |
| `rm -rf project` | force delete | |
| `tmux` | run tmux | |

<br>
<br>

## vim Editor

editing files with vim can make you much much faster.<br>

### Command Mode

This is the mode vim uses when you first enter the buffer area; it is sometimes called normal mode. Here you enter keystrokes to enact commands. For example, pressing the J key will move your cursor down one line. Command is the best mode to use for quickly moving around the buffer area.<br>
| Command | Description | Note |
|---|---|---|
| `h` | Move cursor left one character. |  |
| `l` | Move cursor right one character. |  |
| `j` | Move cursor down one line (the next line in the text). |  |
| `k` | Move cursor up one line (the previous line in the text). |  |
| `w` | Move cursor forward one word to front of next word. |  |
| `e` | Move cursor to end of current word. |  |
| `b` | Move cursor backward one word. |  |
| `^` | Move cursor to beginning of line. |  |
| `$` | Move cursor to end of line. |  |
| `gg` | Move cursor to the file’s first line. |  |
| `G` | Move cursor to the file’s last line. |  |
| `ctrl + B` | Scroll up almost one full screen. |  |
| `ctrl + F` | Scroll down almost one full screen. |  |
| `` |  |  |
| `a` | Insert text after cursor. |  |
| `A` | Insert text at end of text line. |  |
| `dd` | Delete current line. |  |
| `dw` | Delete current word. |  |
| `o` | Open a new text line below cursor, and move to insert mode. |  |
| `p` | Paste copied text after cursor. |  |
| `yw` | Yank (copy) current word. |  |
| `yy` | Yank (copy) current line. |  |
| `x` | to delete the character under the cursor. |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |




<br>


### Insert Mode

Insert Mode Insert mode is also called edit or entry mode. This is the mode where you can perform simple editing. There are not many commands or special mode keystrokes. You enter this mode from command mode by pressing the I key. At this point, the message --Insert-- will display in the message area. You leave this mode by pressing the Esc key.

<br>

### Ex Mode

This mode is sometimes also called colon commands because every command entered here is preceded with a colon (\:). For example, to leave the vim editor and not save any changes you type :q and press the Enter key. <br>

| Command | Description | Note |
|---|---|---|
| `:wq` | Write(Save) and Quit |  |
| `:q` | Quit without Write(Save) |  |
| `:w` | Write buffer to file and stay in editor. |  |

<br>

### vim TIPS

- **Search in vim editor**: If you have a large text file and need to search for something, there are keystrokes in command mode to do that as well. Type ? to start a forward search or / to start a backward search. The keystroke will display at the vim editor’s bottom and allow you to type the text to find. If the first item found is not what you need, press Enter, and then keep pressing the n key to move to the next matching text pattern.

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


## 101 System Architecture
### 101.1 Determine and configure hardware settings

| Path | Description | Note |
|---|---|---|
| `/dev` | Devices | After the Linux kernel communicates with a device on an interface, it must be able to transfer data to and from the device. This is done using device files. Device files are files that the Linux kernel creates in the special /dev directory to interface with hardware devices. <br> As you add hardware devices such as USB drives, network cards, or hard drives to your system, Linux creates a fi le in the /dev directory representing that hardware device. |
| `/proc` | Kernel/process info | The /proc directory is one of the most important tools you can use when troubleshooting hardware issues on a Linux system. It’s not a physical directory on the fi lesystem, but instead a virtual directory that the kernel dynamically populates to provide access to information about the system hardware settings and status. |
| `/sys` | similer to proc | The /sys directory is another virtual directory, similar to the /proc directory. It is created by the kernel in the sysfs filesystem format, and it provides additional information about hardware devices that any user on the system can access. |

| Command | Description |
|---|---|
| `lsblk` | The lsblk command displays information about the block devices installed on the Linux system. By default, the lsblk command displays all block devices. |
| `lspci` | The lspci command allows you to view the currently installed and recognized PCI and PCIe cards on the Linux system. |
| `lsusb` | You can view the basic information about USB devices connected to your Linux system by using the lsusb command. |
| `lsmod` | lists all modules installed on your system. <br> The Linux kernel needs device drivers to communicate with the hardware devices installed on your Linux system. However, compiling device drivers for all known hardware devices into the kernel would make for an extremely large kernel binary file. To avoid that situation, the Linux kernel uses kernel modules, which are individual hardware driver fi les that can be linked into the kernel at runtime |
| `insmod` | The insmod command is the most basic install command, requiring you to specify the exact module file to load. As you’ve seen, the kernel module files are stored in the /lib/modules directory structure, with each kernel version having its own directory. <br> Each file with the .ko extension is a separate module file for each device driver that you can install. To install the module, specify the filename on the insmod command line.|
| `modprobe` | The downside to using the insmod program is that you may run into modules that depend on other modules.The modprobe command helps resolve module dependencies for you. it also understands module names and there is no need for exact nested path to the module. I has many command option. Check it out (`modprobe --help`) |
| `rmmode` | removes a module by specifying the module name. |
| `modprobe -r` | the modprobe command can also remove modules for us, so you don’t need to memorize another command Instead, just use the –r option with the modprobe command |


<br>
<br>
<br>

### 101.2 Boot the System

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 101.3 Change runlevels/boot targets and shutdown or reboot system

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>
<br>
<br>


## 102 Linux Installation and Package Management
### 102.1 Design hard disk layout

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 102.2 Install a boot manager

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 102.3 Manage shared libraries

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 102.4 Use Debian package management

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 102.5 Use RPM and YUM package management

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 102.6 Linux as a virtualization guest

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |


<br>
<br>
<br>
<br>
<br>


## 103 GNU and Unix Commands

| Special characters | Description | Note |
|---|---|---|
| `*?[]'"\$;&()\|^<> ` | these are the special characters in Linux shell. | if you want to use them exactly as they are you should add a \ before them. SPACE is also a special character. Also there is possible to put the word containing a special character or the whole sentence inside two double quotation.  |

| Command | Description | Note |
|---|---|---|
| `echo [OPTION]… [STRING]…` | In the echo command’s syntax structure, [OPTION] means there are various options (also called switches) you can add to modify the display. The [STRING] argument allows you to designate a string to display.  | The brackets indicate that switches are optional. |
| `type NAME_OF_COMMAND` | this command shows that the command written in front of it is a builtin shell command or it is a /usr/bin/NAME_OF_COMMAND |  |
| `cd PATH` | jumps to the directory that we need. |  |
| `uname [OPTION]...` | give data about the system. | it has many options (use --help to see the options). most practical one is -a which shows the whole information about the system. |
| `man NAME_OF_COMMAND` | man is the system's manual pager | you can see what that command does and different options and how to use it...x |
| `VARIABLE_NAME="VALUE"` | we can set variables with a = and then the value for it | example: `PS1="INSERT NEW PROMPT: "` then we can see what each variable value is using the echo command. |
| `history` | keeps track of the history of the prompts we have recently used in command shell. It assignes a number to each of these prompts we used. | using the number assigned to each word, we can reexecute them like this: `!954` |
| ‍‍‍‍`which` |||
| `cat NAME_OF_FILE` OR `batcat NAME_OF_FILE` | view file. |  |
| `paste FILE_1 FILE_2` | view two files side by side. |  |
| `od [OPTION]... FILE` | The od utility can help you to display a file’s contents in octal (base 8), hexadecimal (base 16), decimal (base 10), and ASCII. | By default od displays a fi le’s text in octal. |
| `split [OPTION]... [INPUT [PREFIX]]` | This utility allows you to divide a large file into smaller chunks, which is handy when you want to quickly create a smaller text fi le for testing purposes. | You can divide up a file using size, bytes, lines, and so on. The original file ( INPUT) remains unchanged, and additional new files are created, depending on the command options chosen. |
| `sort [OPTION]... [FILE]...` | it sorts the file alphabetically but doesn't change the input file | use -n option for sorting files containing numbers. |
| `nl [OPTION]... [FILE]...` | This little command allows you to number lines in a text file in powerful ways. | If you do not use any options with the nl utility, it will number only non-blank text lines. If you would like all file’s lines to be numbered, including blank ones, then you’ll need to employ the -ba switch. |
| `more [OPTION] FILE [...]` | One way to read through a large text fi le is by using a pager. a pager option is more.  | With more, you can move forward through a text file by pressing the spacebar (one page down) or the Enter key (one line down). However, you cannot move backward through a file. | 
| `more [OPTION] FILE [...]` | A more flexible pager is the less utility. |  you can move backward and it has more options than more command. |
| `head [OPTION]... [FILE]...` | By default, the head command displays the fi rst 10 lines of a text file. |  |
| `tail [OPTION]... [FILE]...` | By default, the tail command will show a file’s last 10 text lines. |  |
| `wc [OPTION]... [FILE]...` | When you issue the wc command with no options and pass it a filename, the utility will display the file’s number of lines, words, and bytes in that order. |  |
| `md5sum FILE` | The md5sum utility is based on the MD5 message-digest algorithm. it is  excellent for checking a file’s integrity. |  |
| `ls -1 /usr/bin/sha???sum` | shows several utilities thatn implement The Secure Hash Algorithms (SHA) on Linux. These utilities are used in a similar manner to the md5sum command. | for example, `sha256sum FILE` |
| `grep` | A wonderful tool for sifting text |  |
| `tee` | In cases where you want to keep a copy of the command pipeline’s output as well as view it, the tee command will help. The tee command allows you to both save the output to a file and display it to STDOUT. | Similar to a tee pipe fitting in plumbing, where the water flow is sent in multiple directions. |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |
| `` |  |  |




<br>

- **echo TIP**: if you put $ behind a variable you can see the value of that. for example echo $SHELL shows what shell we have in our Linux distro. <br>
  
```bash
echo $SHELL
```
- **cd TIP**: you can have both absolute path (/home/mahan/Books) or a relative path (for example when we are in /usr/bin then we use cd ip it goes to /usr/bin/ip) <br> <br> <br>
- **man TIP**: using / gives us the opportunity to search in the manual. clicking on the n goes to the found in the manual. if you witre a number before a NAME_OF_COMMAND, then you can see that command in another chanter of the manual. <br> <br> <br>
- **Basic regular expressions (BREs)**: include characters, such as a dot followed by an asterisk (.*) to represent multiple characters and a single dot (.) to represent one character. They also may use brackets to represent multiple characters, such as [a,e,i,o,u] (you do not have to include the commas) or a range of characters, such as [A-z]. When brackets are employed, it is called a bracket expression. To find text file records that begin with particular characters, you can precede them with a caret (^) symbol. For finding text file records where particular characters are at the record’s end, append them with a dollar sign ($) symbol. <br> <br> <br>
- **Extended regular expressions (EREs)**: allow more complex patterns. For example, a vertical bar symbol (|) allows you to specify two possible words or character sets to match. You can also employ parentheses to designate additional subexpressions. Use the -E option to indicate the pattern is an extended regular expression. <br> a vertical bar symbol (|) allows you to specify two possible words or character sets to match. You can also employ parentheses to designate additional subexpressions. <br> Use the **-E option** to indicate the pattern is an extended regular expression. If you did not employ the -E option, unpredictable results would occur. for example, `grep -E "^root|^dbus" /etc/passwd` command greps those expressions starting with root OR dbus in /etc/passwd. <br> <br> <br>

- **STDOUT** and **>** and **>>**: The file descriptor that identifies output from a command or script file is 1. It is also identified by the abbreviation STDOUT, which describes standard output. By default, STDOUT directs output to your current terminal. Your process’s current terminal is represented by the /dev/tty file. <br> A redirection operator allows you to change the default behavior of where input and output are sent. For STDOUT, you redirect the output using the > redirection operator. <br> For example, `grep nologin$ /etc/passwd > NologinAccts.txt` command puts the output of the grep to a file named NologinAccts.txt. <br>To append data to a preexisting file, you need to use a slightly different redirection operator. The >> operator will append data to a preexisting file. If the file does not exist, it is created, and the outputted data is added to it. <br> <br> <br> 

- **STDERR** and **2>** and **2>>**: Another handy item to redirect is standard error. The fi le descriptor that identifies a command or script file error is 2. It is also identified by the abbreviation STDERR, which describes standard error. STDERR, like STDOUT, is by default sent to your terminal (/dev/tty).
The basic redirection operator to send STDERR to a file is the 2> operator. If you need to append the file, use the 2>> operator. <br> <br> <br> 

- **/dev/null**: If you don’t care to keep a copy of the error messages, you can always throw them away. This is done by redirecting STDERR to the /dev/null file. The /dev/null file is sometimes called the black hole. This name comes from the fact that anything you put into it, you cannot retrieve. <br> <br> <br> 

- **STDIN** and **\<** and **tr**: Standard input, by default, comes into your Linux system via the keyboard and/or other input devices. The file descriptor that identifies an input into a command or script file is 0. It is also identified by the abbreviation STDIN, which describes standard input. <br> As with STDOUT and STDERR, you can redirect STDIN. The basic redirection operator is the < symbol. The tr command is one of the few utilities that require you to redirect standard input. For example: <br>

```bash
$ cat Grades.txt
89 76 100 92 68 84 73
$
$ tr " " "," < Grades.txt
89,76,100,92,68,84,73
$
```


- **&>** and **&>>**: &> Redirect STDOUT and STDERR to specified file. If file exists, overwrite it. If it does not exist, create it. &>> Redirect STDOUT and STDERR to specified file. If file exists, append to it. If it does not exist, create it. <br> <br> <br>
- **Piping Data**:The pipe is a simple redirection operator represented by the ASCII character 124 (|), which is called the vertical bar, vertical slash, or vertical line. `COMMAND1 | COMMAND2 [| COMMANDN]…` <br> The syntax for pipe redirection shows that the first command, COMMAND1, is executed. Its STDOUT is redirected as STDIN into the second command, COMMAND2. And so on. <br> <br> <br>


<br>
<br>
<br>
<br>
<br>

## 104 Devices, Linux Filesystems, Filesystem Hierarchy Standard
### 104.1 Create partitions and filesystems

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 104.2 Maintain the integrity of filesystems

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 104.3 Control mounting and unmounting of filesystems

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 103.4 Removed

### 104.5 Manage file permissions and ownership

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 104.6 Create and change hard and symbolic links

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 104.7 Find system files and place files in the correct location

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |


<br>
<br>
<br>
<br>
<br>