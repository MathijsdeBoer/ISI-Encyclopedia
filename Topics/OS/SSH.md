---
tags:
  - Shell
  - CLI
  - Networking
  - OS/Windows
  - OS/Linux
  - OS/Mac
aliases:
  - Secure Shell
---

Secure Shell (SSH) is an encrypted network communication protocol that allows users to log into other computers and remotely execute commands.

A typical command to use `ssh` to log into a remote computer looks like this:
`> ssh user@computer`
Where `user` is your username, and `computer` is the name or IP address of the remote computer.

For example:
`> ssh bob@gpuserver`
`> ssh alice@127.0.0.1`
`> ssh charlie@compute.servers.company.com`

The other computer will now ask you to provide your password:
`user@computer's password: _`
Simply type in the password that was provided for you, and hit enter. Don't worry if you don't see anything change when typing. For security reasons, there will be no visual feedback when typing the password.

## First time connecting
When logging into a remote computer for the first time, `ssh` will ask you if you are sure if you want to continue connecting:

```
The authenticity of host 'computer (123.456.78.90)' can't be established.
ECDSA key fingerprint is SHA256:C90NRsN45D9BhSUonjZbKY/nxkPMTXEuTRsC1yUXcu8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? _
```

This is simply `ssh` telling you that you've never connected to this particular server before. This is a security feature. If you suddenly get this message again from connecting to a server that you've used often before, you know that _something_ has changed on the other end. Either through a simple reconfiguring of the other computer, or someone has started spoofing the server's identity.

To accept the request, simply type `yes` and hit enter.

