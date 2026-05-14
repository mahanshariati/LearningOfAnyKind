# LPIC 1

- [LPIC 1](#lpic-1)
  - [useful tips:](#useful-tips)
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
    - [103.1 Work on the command line](#1031-work-on-the-command-line)
    - [103.2 Process text streams using filters](#1032-process-text-streams-using-filters)
    - [103.3 Perform basic file management](#1033-perform-basic-file-management)
    - [103.4 Use streams, pipes and redirects](#1034-use-streams-pipes-and-redirects)
    - [103.5 Create, monitor and kill processes](#1035-create-monitor-and-kill-processes)
    - [103.6 Modify process execution priorities](#1036-modify-process-execution-priorities)
    - [103.7 Search text files using regular expressions](#1037-search-text-files-using-regular-expressions)
    - [103.8 Basic file editing](#1038-basic-file-editing)
  - [104 Devices, Linux Filesystems, Filesystem Hierarchy Standard](#104-devices-linux-filesystems-filesystem-hierarchy-standard)
    - [104.1 Create partitions and filesystems](#1041-create-partitions-and-filesystems)
    - [104.2 Maintain the integrity of filesystems](#1042-maintain-the-integrity-of-filesystems)
    - [104.3 Control mounting and unmounting of filesystems](#1043-control-mounting-and-unmounting-of-filesystems)
    - [103.4 Removed](#1034-removed)
    - [104.5 Manage file permissions and ownership](#1045-manage-file-permissions-and-ownership)
    - [104.6 Create and change hard and symbolic links](#1046-create-and-change-hard-and-symbolic-links)
    - [104.7 Find system files and place files in the correct location](#1047-find-system-files-and-place-files-in-the-correct-location)


## useful tips:
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
### 103.1 Work on the command line

| Special characters | Description | Note |
|---|---|---|
| `* ? [ ] ' " \ $ ; & ( ) \| ^ < >` | these are the special characters in Linux shell. | if you want to use them exactly as they are you should add a \ before them. |

| Command | Description | Note |
|---|---|---|
| `echo [OPTION]… [STRING]…` | In the echo command’s syntax structure, [OPTION] means there are various options (also called switches) you can add to modify the display. The [STRING] argument allows you to designate a string to display.  | The brackets indicate that switches are optional. |
| `type NAME_OF_COMMAND` | this command shows that the command written in front of it is a builtin shell command or it is a /usr/bin/NAME_OF_COMMAND |  |
| `cd PATH` | jumps to the directory that we need. |  |
| `uname [OPTION]...` | give data about the system. | it has many options (use --help to see the options). most practical one is -a which shows the whole information about the system. |
| `man NAME_OF_COMMAND` | man is the system's manual pager | you can see what that command does and different options and how to use it...x |
<br>

- **echo TIP**: if you put $ behind a variable you can see the value of that. for example echo $SHELL shows what shell we have in our Linux distro. <br>
  
```bash
echo $SHELL
```
- **cd TIP**: you can have both absolute path (/home/mahan/Books) or a relative path (for example when we are in /usr/bin then we use cd ip it goes to /usr/bin/ip) <br>
- **man TIP**: using / gives us the opportunity to search in the manual. clicking on the n goes to the found in the manual. if you witre a number before a NAME_OF_COMMAND, then you can see that command in another chanter of the manual. <br>



<br>
<br>
<br>

### 103.2 Process text streams using filters

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 103.3 Perform basic file management

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 103.4 Use streams, pipes and redirects

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 103.5 Create, monitor and kill processes

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 103.6 Modify process execution priorities

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 103.7 Search text files using regular expressions

| Path | Description | Note |
|---|---|---|
| `` |  |  |

| Command | Description | Note |
|---|---|---|
| `` |  |  |

<br>
<br>
<br>

### 103.8 Basic file editing

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