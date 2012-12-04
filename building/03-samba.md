# SMB Server Setup

This document covers setting up a
[Server Message Block (SMB)](http://en.wikipedia.org/wiki/Server_Message_Block)
server into the Virtual Machine. SMB is used to share the VM's filesystem with
Windows hosts, because Windows does not have an
[sshfs](http://fuse.sourceforge.net/sshfs.html) implementation.

These steps should not be performed on a real server, because the setup is
terribly insecure, for development convenience. If the VM will not be used in
Windows, these steps are also not necessary.


## Packages and Configuration

1. Install the [Samba](http://www.samba.org/) packages.

```bash
sudo apt-get install -y samba
```

1. Edit the Samba configuration file. (replace `vim` with `nano` if you're not
   a vim user)

```bash
sudo vim /etc/samba/smb.conf
```

1. Find each of the lines below in the configuration file.

```
   workgroup = WORKGROUP
;   interfaces = 127.0.0.0/8 eth0
;   bind interfaces only = yes
```

1. Replace the lines you found with the lines below.

```
   workgroup = SIX470
   interfaces = eth1
   bind interfaces only = yes
```

1. Add the following section at the end of the configuration file.

```
[files]
  comment = MIT 6.470 Development VM Files
  path = /
  browseable = yes
  read only = no
  guest ok = no
  create mask = 0755
  directory mask = 0755
  force user = six470
  force group = six470
```

1. Set up the SMB password for `six470` to match the main password.

```bash
sudo smbpasswd -a six470
```

1. Type `webdev` at the two password prompts shown below.

```
New SMB password:
Retype new SMB password:
```

### Commentary

This configuration is roughly equivalent to connecting as the `six470` user
over sshfs, modulo whatever security issues the Samba server might have. Samba
is explictly configured to listen to `eth1` to work around the VirtualBox bug
that causes multicast traffic to spill over the wrong side of a NAT interface.

The setup can probably be stripped down to reduce RAM usage and lock down the
server. Contributions are welcome.
