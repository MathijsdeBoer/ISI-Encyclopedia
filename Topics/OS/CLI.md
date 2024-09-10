---
tags:
  - CLI
  - OS
  - Shell
---
The Command Line Interface (CLI) is a general term for programs that let you interact with your operating system through a text interface. These emerged in the 1960s as a means to more conveniently interact with the large computer systems of the time, superseding the punch cards. The modern form of interaction with a computer is mostly done through the Graphical User Interface (GUI).

Generally, we can split a CLI into two main types:
- Operating System (OS) CLI
- Application CLI
The OS CLI is commonly pre-packaged with the OS and lets the user interact with system features or applications, whereas an Application CLI is more restricted to the relevant application.

Which OS CLI you use is dependent on the OS of the machine you're interacting with, and personal preference. 

For Windows, think of CMD or PowerShell. Whereas CMD has been around since 1987, PowerShell is much newer with a first release in 2006. For new users and projects, Microsoft has decided in 2016 that PowerShell shall be the new default terminal application in Windows ([resulting in a small panic that CMD was getting removed](https://devblogs.microsoft.com/commandline/rumors-of-cmds-death-have-been-greatly-exaggerated/)). PowerShell's functionality is much more in line with other terminals, and it contains a few more modern nice-to-haves that cmd does not have.

Linux and macOS systems share a lot of underlying architecture, so their CLI shells are fairly interchangeable. What you'll often find on these is either `sh` or `bash`, whereas macOS has switched to `zsh` since the Catalina update. There are more shells that you can install to your own liking, such as `fish`. 

Excluding CMD, all presented shells share a similar basic usage:
```shell
# Change directory to
# - .../...
cd .../...

# - one directory up
cd ..

# - root (linux/macOS)
cd /

# - drive root (Windows)
cd c:/

# List files and directories in:
# - current directory
ls

# - the given directory
ls .../...

# - the current directory, including hidden
ls -a

# Run program in current directory
# - linux/macOS
./program

# - Windows (.exe at the end optional)
program[.exe]
```
Whereas small differences here and there exist, and given that there are a lot more functions you can call, it should be clear that there aren't many functional differences (anymore) between the terminals.