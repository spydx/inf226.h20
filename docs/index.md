## Welcome to INF226

[UiB: Subject link](www.uib.no/emne/INF226)

## Mandatory 1

### Setup

You will need a Linux system.
macOs will not work as the binaries for the assignment is compiled for Linux.

But installing Linux in a Virtual Machine will work.
Choose your distro.
Windows users have the option of installing WSL2 (described under) or use a VM.

### Windows Subsystem for Linux

If you have a Windows 10 Machine and don't wanna run a linux distro in a Virtual Machine.

It has been tested and verified that pwntools work on WSL2 w/Ubutntu installation.

[Windows Subsystem for Linux Install Guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

Important that you follow all the instructions in this quide if you wanna install WSL2.

[Updating the WSL2 2 Linux kernel](https://docs.microsoft.com/en-us/windows/wsl/wsl2-kernel)

When you have installed WSL you can access the Windows Subsystem for Linux this way:

```cmd
PS> wsl
```

## Tools

### PwnTools

[PwnTools Installation Instructions](http://docs.pwntools.com/en/latest/install.html)

[PwnTools Documentation](http://docs.pwntools.com/en/stable/intro.html)

Is installed on Linux or in WSL2 the following way from the terminal.

```sh
$> sudo apt-get update
$> sudo apt-get install python3 python3-pip python3-dev git libssl-dev libffi-dev build-essential
$> python3 -m pip install --upgrade pip
$> python3 -m pip install --upgrade pwntools
```

### gdb

Installing if it is not already there.

```sh
$ sudo apt-get update
$ sudo apt-get install gdb
```

Usefull commands
```sh
info func # list all functions
run # runs main
step # step through
break *address # set a breakpoint
```

[GDB Manual](https://ftp.gnu.org/old-gnu/Manuals/gdb/html_node/gdb_toc.html)




### Other fansy and maybe usefull resources

[Convert Unicode to Bytes](https://onlineunicodetools.com/convert-unicode-to-bytes)