## Installing

On Ubuntu:

`sudo apt-get install lxd`

`sudo apt-get install lxc`

Now check status :

`systemctl status snap.lxd.daemon`

`systemctl status lxc`

Start LXD:

`systemctl start snap.lxd.daemon`

Add your user:

If you want to run your lxc command without using `sudo` everytime, you should
have your user name in lxd group. To check:

`getent group lxd`

output:

`lxd:x:131:dhaval`

here `dhaval` is my username, that is already made part of lxd group at the installation time.
In case your user is not part of the group then you can add it using 

`sudo gpasswd -a dhaval lxd`

preferrably, logout and log back in so that changes can take effect.

## Initialize lxd

```

dhaval@thinkpad:~/IdeaProjects/Janssen$ lxd init
Would you like to use LXD clustering? (yes/no) [default=no]: 
Do you want to configure a new storage pool? (yes/no) [default=yes]: 
Name of the new storage pool [default=default]: 
Name of the storage backend to use (btrfs, dir, lvm, ceph) [default=btrfs]: dir
Would you like to connect to a MAAS server? (yes/no) [default=no]: 
Would you like to create a new local network bridge? (yes/no) [default=yes]:         
What should the new bridge be called? [default=lxdbr0]: 
What IPv4 address should be used? (CIDR subnet notation, “auto” or “none”) [default=auto]: 
What IPv6 address should be used? (CIDR subnet notation, “auto” or “none”) [default=auto]: 
Would you like the LXD server to be available over the network? (yes/no) [default=no]: 
Would you like stale cached images to be updated automatically? (yes/no) [default=yes]     
Would you like a YAML "lxd init" preseed to be printed? (yes/no) [default=no]: 
dhaval@thinkpad:~/IdeaProjects/Janssen$ 

```
  
  



