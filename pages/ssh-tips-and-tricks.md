---
title: SSH Tips and Tricks
description: "Awful Joke: What do you call a group of people who use SSH without passwords? An open party!"
published: true
categories:
    - Tech
type: pages
layout: pages
date: 2025-04-03T21:24:58.915Z
lastmod: 2025-05-25T04:50:22.623Z
tags:
    - Linux
    - Windows
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
keywords:
    - SSH
    - SSHD
---

<!--- cSpell:disable --->
* [SSH Client](#ssh-client)
  * [Port Forwarding](#port-forwarding)
  * [Reverse Port Forwarding](#reverse-port-forwarding)
* [SSH Keys](#ssh-keys)
  * [Copying others authorized\_keys file](#copying-others-authorized_keys-file)
* [SSHD](#sshd)
  * [AllowGroups](#allowgroups)
* [SSH on Windows](#ssh-on-windows)
* [SSHD on Windows](#sshd-on-windows)
* [Tools](#tools)
* [References](#references)
<!--- cSpell:enable --->

## SSH Client

`ssh username@host`\
`ssh username@host -p customportno`\
`ssh username@host -i /path/to/identitykey`\
`ssh username@host -J jumpusername@jumphost:jumpport`\
`ssh username@host -B eth0`: bind to an interface\
`ssh username@host -b 192.168.1.25`: bind to an ip address\
`ssh username@host -v`: verbose - useful for diagnosing automation and auth issues.

* [x] port forwarding commands
* [x] reverse port forward commands
* [ ] add in commands and info for control socket connection sharing (ControlPath and ControlMaster)
* [ ] tunnel commands

### Port Forwarding

To forward a local port (say 5110) to a remote destination (say popserver.example.com port 110), you can write something like one of these:

```bash
ssh username@host -L 5110:popserver.example.com:110
ssh username@host -L 8080:webserver.example.com:80
ssh username@host -L 8443:192.168.1.1:443
```

To specify an IP address for the listening end of the tunnel, prepend it to the argument:

`ssh username@host -L 127.0.0.5:23:localhost:23 myhost`

From the SSH man page:

> ```bash
> ssh username@host -L [bind_address:]port:host:hostport
> ssh username@host -L [bind_address:]port:remote_socket
> ssh username@host -L local_socket:host:hostport
> ssh username@host -L local_socket:remote_socket
> ```
>
> Specifies that connections to the given TCP port or Unix socket on the local (client) host are to be forwarded to the given host and port, or Unix socket, on the remote side.  This works by allocating a socket to listen to either a TCP port on the local side, optionally bound to the specified bind_address, or to a Unix socket.  Whenever a connection is made to the local port or socket, the connection is forwarded over the secure channel, and a connection is made to either host port hostport, or the Unix socket remote_socket, from the remote machine.
>
> Port forwardings can also be specified in the configuration file.  Only the superuser can forward privileged ports.  IPv6 addresses can be specified by enclosing the address in square brackets.
>
> By default, the local port is bound in accordance with the GatewayPorts setting.  However, an explicit bind_address may be used to bind the connection to a specific address.  The bind_address of "localhost" indicates that the listening port be bound for local use only, while an empty address or '*' indicates that the port should be available from all interfaces.

### Reverse Port Forwarding

To forward a remote port to a local destination, just use the -R option instead of -L:

```bash
ssh username@host -R 5023:mytelnetserver.myhouse.org:23
```

From the SSH man page:

> ```bash
> ssh username@host -R [bind_address:]port:host:hostport
> ssh username@host -R [bind_address:]port:local_socket
> ssh username@host -R remote_socket:host:hostport
> ssh username@host -R remote_socket:local_socket
> ssh username@host -R [bind_address:]port
> ```
>
> Specifies that connections to the given TCP port or Unix socket on the remote (server) host are to be forwarded to the local side.
>
> This works by allocating a socket to listen to either a TCP port or to a Unix socket on the remote side.  Whenever a connection is made to this port or Unix socket, the connection is forwarded over the secure channel, and a connection is made from the local machine to either an explicit destination specified by host port hostport, or local_socket, or, if no explicit destination was specified, ssh will act as a SOCKS 4/5 proxy and forward connections to the destinations requested by the remote SOCKS client.
>
> Port forwardings can also be specified in the configuration file. Privileged ports can be forwarded only when logging in as root on the remote machine.  IPv6 addresses can be specified by enclosing the address in square brackets.
>
> By default, TCP listening sockets on the server will be bound to the loopback interface only.  This may be overridden by specifying a bind_address.  An empty bind_address, or the address '*', indicates that the remote socket should listen on all interfaces.  Specifying a remote bind_address will only succeed if the server's GatewayPorts option is enabled (see sshd_config(5)).
>
> If the port argument is '0', the listen port will be dynamically allocated on the server and reported to the client at run time.  When used together with -O forward, the allocated port will be printed to the standard output.

## SSH Keys

* [ ] Add in SSH Keygen stuff
* [ ] Add in ssh-copy-id stuff
* [ ] Add in authorised keys file management tips
* [ ] ssh agent key forwarding stuff but also ssh agent key forwarding security risks

### Copying others authorized_keys file

```bash
# on host 1:
sudo scp /home/otheruser/.ssh/authorized_keys myusername@host2:/home/myusername/otheruser-authorized_keys

# on host 2 - Updating existing authorized_keys file:
sudo cat /home/myusername/otheruser-authorized_keys >> /home/otheruser/.ssh/authorized_keys

# on host 2 - never logged in before authorized_keys file:
sudo mkdir /home/otheruser/.ssh/
sudo chown otheruser:otheruser /home/otheruser/.ssh/
sudo chmod 0700 /home/otheruser/.ssh/
sudo mv ~/otheruser-authorized_keys /home/otheruser/.ssh/authorized_keys
sudo chown otheruser:otheruser /home/otheruser/.ssh/authorized_keys
sudo chmod 0600 /home/othersuer/.ssh/authorized_keys

# on host - never logged in before (suggestion from a friend)
sudo install -d -m 700 -o otheruser -g otheruser /home/otheruser/.ssh
echo "ssh-ed25519 AAAA... comment" | sudo tee /home/otheruser/.ssh/authorized_keys > /dev/null
sudo chown otheruser:otheruser /home/otheruser/.ssh/authorized_keys
sudo chmod 600 /home/otheruser/.ssh/authorized_keys
```

This answer has a lot: <https://askubuntu.com/a/875058/443835>

## SSHD

`sudo sshd -T`:Show sshd current **running** config

<https://documentation.ubuntu.com/server/how-to/security/openssh-server/>

### AllowGroups

Based off: <https://documentation.ubuntu.com/server/how-to/security/user-management/#:~:text=Restrict%20SSH%20access%20to%20only%20user%20accounts%20that%20should%20have%20it>

```bash
sudo addgroup sshlogin
sudo adduser yourusernamehere sshlogin # add your login to the group
sudo adduser anotherusernamehere sshlogin # add other user to the group
sudo adduser anotherusernamehere sudo # *IF* user also needs sudo
#sudo useradd -m -G sshlogin,sudo XXX -s /bin/bash # alternative way modify existing user
#sudo passwd XXX # if you need to change user's password
sudo cp /etc/ssh/sshd_config ~/ # backup sshd_config
sudo vi /etc/ssh/sshd_config
```

Make the following changes to sshd_config:

```txt
# You may need to do these commands at a later stage to prevent initial build issues (password auth mostly) but they must be done before it goes live
PermitRootLogin no
AllowGroups sshlogin
PasswordAuthentication no
```

`sudo systemctl restart sshd.service`

## SSH on Windows

TBC

## SSHD on Windows

TBC

## Tools

<https://www.harding.motd.ca/autossh/>

## References

[PuTTY Commands](putty-commands.md)

[SSH man page](https://linux.die.net/man/1/ssh)

<https://en.wikibooks.org/wiki/OpenSSH>\
<https://en.wikibooks.org/wiki/OpenSSH#:~:text=Development-,Cookbook,-%5Bedit%20%7C>\
<https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Proxies_and_Jump_Hosts#Passing_Through_One_or_More_Gateways_Using_ProxyJump>
