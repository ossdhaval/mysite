# VMWare Player

## how can you make two running VMs talk to each other
Short answer is that VMs that you created with default configuration will be able to talk to each other automatically. Talk here means being
able to access each other via IP. Plus, the ports like 80 and 443 are already open. So, basically IP of VMs are visible from base OS as well as each 
other. In the default configuration, network adapter is in NAT mode.

## Troubleshooting VMware player error on Ubuntu
error is about vmmon and vmnet modules when you try to start vmware on ubuntu. Solution: https://askubuntu.com/a/1145426

## about VM tools
To see vm scree in full screen resolution, you need vmware tools installed on that vm. Using

```
sudo apt-get update
sudo apt install open-vm-tools-desktop
```
