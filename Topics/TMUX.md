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
## Controls
