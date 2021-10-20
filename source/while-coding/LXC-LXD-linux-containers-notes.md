# LxC - LxD linux container notes

### References
- https://www.youtube.com/watch?v=kXBsghAug2c
- https://discuss.linuxcontainers.org/t/solved-static-ip-address-to-lxc-container/7704

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

### Steps to create and setup an lxc container
1) select linux distribution from https://uk.images.linuxcontainers.org/. Note down values in first three columns of the container that you want (distribution, release, architecture) and then run 
    ```
    sudo lxc launch images:ubuntu/focal/amd64 my-ubuntu-container
    ```
2) list your container using `lxc ls`
3) to get into container shell `lxc exec my-ubuntu-container bash`
4) to see the files in container `cd ..` and then `ls`
5) now to be able to connect to container directly via ssh (and not via `lxc` command), we need to install ssh server on container using `sudo apt install openssh-server`
6) create a new user `add user dev`
7) restart sshd service `service restart sshd`
8) Now to connect to container from other PC using ssh and the newly created user you have to use: `sudo ssh dev@<ip>`. This ip is internal IP of the container. If can be found by logging into container using lxc command and then firing `ip a`. Output will be something like this
    ```
    root@my-ubuntu-container:~# ip a
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host 
           valid_lft forever preferred_lft forever
    7: eth0@if8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
        link/ether 00:16:3e:09:dc:5c brd ff:ff:ff:ff:ff:ff link-netnsid 0
        inet 10.229.38.143/24 brd 10.229.38.255 scope global dynamic eth0
           valid_lft 3288sec preferred_lft 3288sec
        inet6 fd42:7394:a42:7262:216:3eff:fe09:dc5c/64 scope global dynamic mngtmpaddr noprefixroute 
           valid_lft 3158sec preferred_lft 3158sec
        inet6 fe80::216:3eff:fe09:dc5c/64 scope link 
           valid_lft forever preferred_lft forever
    ```
    from this, you have to pick up `10.229.38.143` ip. Now from local PC you can run `sudo ssh dev@10.229.38.143` to login to container.
6) Now, to install a web server on container and access that web page from local machine 
    - first login to container as root using `lxc exec my-ubuntu-container bash`
    - then install apache server `sudo apt install apache2`
    - check if apache service is running `service apache2 status`
    - now go to your local machine, open browser and try to hit the IP of the container `10.229.38.143`
