---
tags:
  - CLI
  - OS/Linux
  - Shell
---
`tmux` is a terminal multiplexer for Unix-like operating systems. Effectively, it turns your [[CLI]] into a tiled set of smaller CLI sessions. An important feature of `tmux` is that it detaches the running processes from the controlling terminals, which allows for remote sessions to keep running after a disconnect.

`tmux` maintains a hierarchy of concepts. At the top we have the session, which houses windows, and each window is split up in panes.
```
Session
|-- Window
	|- Pane
|-- Window
	|-- Pane
	|-- Pane
	...	
```

A useful resource is the [TMUX Cheat Sheet website](https://tmuxcheatsheet.com/), which lists a much more comprehensive set of controls than what we cover in this document.
## Sessions
Sessions are the overarching concept within `tmux`. They manage active windows in neatly organized groupings.

Starting a `tmux` session can be as easy as simply typing
`> tmux`
in a terminal. This will create a new session, and open a window for you. However, if you've already got an earlier session running, you can reconnect to it with
`> tmux attach`
If you've got _multiple_ sessions running, you can list them with
`> tmux ls`
and connect to a specific one with
`> tmux attach -t [session]`

Closing a session can be as easy as typing
`> exit`
in the session's last existing window. If you have multiple windows open, it'll close the window, but keep the remaining one(s). Only when you type the `exit` command in the last one will it also close the session. If you want to kill a session without entering it, you can use
`> tmux kill-session -t [session]`
## Basic usage
While there are a lot of features in `tmux`, the basic things to remember are actually quite simple. When using the keyboard in a `tmux` session, all keystrokes are sent to the terminal that is currently active. If you want to interact with the `tmux` session itself, you'll need to input the escape sequence. By default, this is `Ctrl + B`. After pressing this combination, you might see nothing change, that is because `tmux` is now awaiting your next input. Some example inputs:
- `Ctrl + B, D`
  Detach from the session
- `Ctrl + B, [↑ ↓ → ←]`
  Change active pane. If you don't select another direction in a short amount of time the currently selected pane will become active
- `Ctrl + B, [`
  Allows you to scroll through the terminal's history with `↑` and  `↓`. Hold `Ctrl` while scrolling for moving the entire pane one line at a time, and hold `Alt` to jump several. Depending on the installed version of `tmux`, you can also scroll with the mouse wheel.
- `Ctrl + B, Ctrl + [↑ ↓ → ←]`
  Resize the currently active pane in the direction you tap. Keep holding `Ctrl` while tapping a direction to make multiple adjustments. Releasing `Ctrl` will stop resizing again.