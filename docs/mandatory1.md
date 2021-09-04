# INF226 Support Material

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

### macOS

There is a solution to run linux tools, binaries and pwntools through Docker on macOs. (no need for VM)

[Download Docker for macOS](https://www.docker.com/products/docker-desktop)

[Install and run (first time)](https://hub.docker.com/repository/docker/spydx/inf226)

```sh
docker pull spydx/inf226:latest
docker run -v /Users:/mnt/Users/ -w /mnt/Users/ -it --name inf226 spydx/inf226:latest
```

To run after first time
```sh
docker start -i inf226
```

There are probalbly many limitations to this or issues, but I managed to run, and use GDB to analyse binaries this way.


## Tools

Listed from the slides

* `gcc` - A C compiler
* `gdb` - A debugger
* `objdump -d` - A dissasembler
* `xxd` - converting between hex and bytes
* `strace` - Make a log of the systemcalls made by the process

### `binutils`

Some places it is mentioned that you need to install binutils.
If your distrubution doesn't have that, this means that gdb, gcc, objdump is not preinstalled. Some Linux distros come without, my Ubuntu install they are preinstalled.

To install binutils:

```sh
>sudo apt-cache update
>sudo apt-get install binutils
```

Information about common tools in bin utils
[Binutils](https://www.gnu.org/software/binutils/binutils.html)

### PwnTools

[PwnTools Installation Instructions](http://docs.pwntools.com/en/latest/install.html)

[PwnTools Readme (Github)](https://github.com/Gallopsled/pwntools-tutorial#readme)

[PwnTools Documentation](http://docs.pwntools.com/en/stable/intro.html)

Is installed on Linux or in WSL2 the following way from the terminal.

```sh
$> sudo apt-get update
$> sudo apt-get install python3 python3-pip python3-dev git libssl-dev libffi-dev build-essential
$> python3 -m pip install --upgrade pip
$> python3 -m pip install --upgrade pwntools
```

If you get import problems with `pwntools`, please verify that you are using `python3` when you run the script.

```sh
> python --version # should be version 3
```

If `python` is 2.x use `python3` cmd instead.

If you have linting problems in VSCode, check that you are using the correct interperator in python.


```python
from pwn import *
# Open the program with a gdb wrapper
# Here you can add a second argument that is a string and containing gdb
# commands you want to run in the gdb interpreter.
# Once the window has opened, you can simply type "c" for "continue" to
# continue executing. You can do your gdb stuff in the new window.
p = gdb.debug('./1')
# To open a process instead uncomment this and comment above initialization of
# p:
# p = process('./1')
# To connect to the remote instead, uncomment this and comment above
# initialization of p:
# p = remote('ctf21.softwaresecurity.no', 9001)
# Send some line of input to the process
p.sendline(b'Someinput')
# Read from the process until "get past me" is displayed
print(p.recvuntil(b'get past me'))
# Use interactive to interact manually with the program again
p.interactive()
# Close the process at the end
p.close()
```

For people working in WSL, you might want to first run the `tmux` command and run your script within it.
You'll ned to add `context.terminal = ["tmux", "splitw", "-h"]` before you initialize p.

#### Debugging trick

```python
from pwn import *
p = gdb.debug(<binary_name_as_string>, <gdb_commands_to_exec_automatically_as_string>)
```

[PwnTools: GDB](https://docs.pwntools.com/en/stable/gdb.html)

#### macOS notes

You will not be able to use gdb or similar tools to run the binaries on macOS

You can install pwntools on macOS either throug [Homebrew](https://brew.sh/)

```sh
> /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
> brew install pwntools
```

or just install the library:

```sh
> python3 -m pip install --upgrade pwntools
```

This will help you atleast to write the script and run the attack from your mac instead of inside the virtual machine :)

### `gdb`

Installing if it is not already there.

```sh
$ sudo apt-get update
$ sudo apt-get install gdb
```

#### Useful commands

```sh
info func # list all functions
run # runs main
step # step through
break *address # set a breakpoint
```

[CFT101 Guide for GDB](https://ctf101.org/reverse-engineering/what-is-gdb/)
[GDB Manual](https://ftp.gnu.org/old-gnu/Manuals/gdb/html_node/gdb_toc.html)

[GDB breakpoints](https://ftp.gnu.org/old-gnu/Manuals/gdb/html_node/gdb_28.html#SEC29)

Setting breakpoints on of the options

```sh
gdb > br *<addr>
gdb > br symbol
```

Common issue is missing execute rights on the binary.

```sh
> ./<filename>
Error Access denied
>
```

Check for `+x` and solve it this way.

```sh
> ls -la <filename>
-rw-rw--- <filename> #verified that is its missing +x
> chmod +x <filename>
> ls -la <filename>
-rw-rw---x <filename> # now you should be able to run it
```

### `xxd`

[xxd manual](http://manpages.ubuntu.com/manpages/precise/man1/xxd.1.html)

### `objdump`

Create a dissasembly output of the program

```sh
objdump -d > file.txt
```

### `checksec`

`checksec` is used to check what security settings are available.

[GitHub for `checksec`](https://github.com/slimm609/checksec.sh)

### Other fancy and maybe useful resources

* [CTF Intro to C](https://ctf101.org/reverse-engineering/what-is-c/)
* [CTF Binary Exploitation](https://ctf101.org/binary-exploitation/overview/)
* [Buffer Overflows](https://ctf101.org/binary-exploitation/buffer-overflow/)
* [Return Oriented Programming](https://ctf101.org/binary-exploitation/return-oriented-programming/)
* [Bypassing Stack Canaries](https://ctf101.org/binary-exploitation/stack-canaries/)
* [Convert Unicode to Bytes](https://onlineunicodetools.com/convert-unicode-to-bytes)
