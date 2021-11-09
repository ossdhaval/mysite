# LxC - LxD linux container notes

### References
- https://www.youtube.com/watch?v=kXBsghAug2c
- https://discuss.linuxcontainers.org/t/solved-static-ip-address-to-lxc-container/7704
- lxc commands: https://linuxcontainers.org/lxd/getting-started-cli/#instance-management

## what is LxC and LxD
- LxC (LinuX Container)
- LxD (Lx Deamon)

For long version read [this](https://linuxcontainers.org/) and for differences read [this](https://discuss.linuxcontainers.org/t/comparing-lxd-vs-lxc/24)

In short:

LxC is core containerization which is used by LxD(which is newer and makes LxC containerization more user friendly). LxD uses LxC underneath. Recommendation for all new users is to use LxD unless there is a special need of using LxC directly.
For commandline, there is a confusion caused by name of lxd client, which is called `lxc`. This gets confused with `lxc` containers. You'll find two sets of commands like `lxc start` and also `lxc-start`. Remember that `lxc start` is LxD command and `lxc-start` is an LxC command. Try to stick to first version so you continue to use LxD.

## Installing

On Ubuntu:

```
sudo apt-get install lxd
```

Now check status :

```
systemctl status snap.lxd.daemon
```


Start LXD:

```
systemctl start snap.lxd.daemon
```


Add your user:

If you want to run your lxc command without using `sudo` everytime, you should
have your user name in lxd group. To check:

```
getent group lxd
```

output:

```
lxd:x:131:dhaval
```

here `dhaval` is my username, that is already made part of lxd group at the installation time.
In case your user is not part of the group then you can add it using 

```
sudo gpasswd -a dhaval lxd
```

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
6) create a new user `adduser dev`
7) restart sshd service `service sshd restart`
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
9) Now, to install a web server on container and access that web page from local machine 
    - first login to container as root using `lxc exec my-ubuntu-container bash`
    - then install apache server `sudo apt install apache2`
    - check if apache service is running `service apache2 status`
    - now go to your local machine, open browser and try to hit the IP of the container `10.229.38.143`. You should be able to access default apache page

10) if you want to create a shared folder between local computer and container
    - from local machine run `sudo lxc config device add my-ubuntu-container shared_dir disk path=/var/www/localhost/htdocs source="/home/nevyan/web_dev"`
    - above command will map content of local directory `/home/nevyan/web_dev` to `/var/www/localhost/htdocs` directory within the container

11) you can delete this container
    `lxc delete my-ubuntu-container`

Note: 

    1) in my case IP address when run `lxc ls` from local machine and address from running `ip a` from within container are same
    
    2) This ip address stayed static even after stopping and starting container as well as local machine.
    

### creating a reusable image from container

The easiest way by far to build an image with LXD is to just turn a container into an image.

This can be done with:

```
lxc launch ubuntu:14.04 my-container
lxc exec my-container bash
<do whatever change you want>
lxc publish my-container --alias my-new-image
```

You can even turn a past container snapshot into a new image:

`lxc publish my-container/some-snapshot --alias some-image`

Now you can see this image in the list of available images:

`lxc image list`

you can create new containers from this image:

`lxc launch image-name container-name`

### creating lxc with ip mapping
    
```
snap install lxd
snap refresh
lxd init # Default settings looks good. I only specifid dir storage method to access container filesystem /var/snap/lxd/common/lxd/storage-pools/default/containers/ubuntu20/rootfs/
lxc launch images:ubuntu/20.04/amd64 ubuntu20
lxc config device add ubuntu20 myport443 proxy listen=tcp:0.0.0.0:443 connect=tcp:127.0.0.1:443
lxc config device add ubuntu20 myport1636 proxy listen=tcp:0.0.0.0:1636 connect=tcp:127.0.0.1:1636
lxc config set ubuntu20 limits.memory 4GB
```

to login

`lxc exec ubuntu20 -- sudo --user root --login`
or 
`lxc exec ubuntu20 -- /bin/bash`

### important commands:

- `lxc start <cntr-name>`
- `lxc stop <cntr-name>`
- `lxc config device add <cntr-name> myport443 proxy listen=tcp:0.0.0.0:443 connect=tcp:127.0.0.1:443`
- `lxc config device add <cntr-name> myport1636 proxy listen=tcp:0.0.0.0:1636 connect=tcp:127.0.0.1:1636`
