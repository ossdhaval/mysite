# Random notes

### Troubleshooting VMware player error on Ubuntu
error is about vmmon and vmnet modules when you try to start vmware on ubuntu.
Solution: 
first : https://communities.vmware.com/t5/VMware-Workstation-Pro/VMware-16-2-3-not-working-on-Ubuntu-22-04-LTS/m-p/2905637/highlight/true#M175412
second : https://askubuntu.com/a/1145426

These instructions have been tested for VMWare player 16.2.1 and Ubuntu 18.04 up to 19.04.

Install VMWare
Run this

```
cd /usr/lib/vmware/modules/source
sudo git clone https://github.com/mkubecek/vmware-host-modules
cd vmware-host-modules
sudo git checkout player-16.2.1
sudo make
sudo tar -cf vmnet.tar vmnet-only
sudo tar -cf vmmon.tar vmmon-only
sudo mv vmnet.tar /usr/lib/vmware/modules/source/
sudo mv vmmon.tar /usr/lib/vmware/modules/source/
```

```
sudo vmware-modconfig --console --install-all
```

You'll see that there are issues with monitor and net, thas ok.

Generate a key

```
openssl req -new -x509 -newkey rsa:2048 -keyout VMWARE15.priv -outform DER -out VMWARE15.der -nodes -days 36500 -subj "/CN=VMWARE/"
```

You'll see info that it did it ok.

Use this key we just generated to sign the two kernel modules.

```
sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 ./VMWARE15.priv ./VMWARE15.der $(modinfo -n vmmon)
sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 ./VMWARE15.priv ./VMWARE15.der $(modinfo -n vmnet)
```

This does not give any feedback

Check that signatures are applied correctly.

```
tail $(modinfo -n vmmon) | grep "Module signature appended"
```
You should get Binary file (standard input) matches

Now we make this key trusted by importing it to machine owner key (MOK) management system with the command below. Here you can read more about MOK’s job in Linux.

```
sudo mokutil --import VMWARE15.der
```
This will ask you for a password, enter some new password a bit long like 1515vmware. Reenter same password.

Reboot, When reboot you should be presented with a menu with blue screen background, you have to make your way to enroll the key and enter the password you just created, this happens only once, then continue to boot.

To test the driver / module installed correctly enter the command

```
mokutil --test-key VMWARE15.der
```
You should get VMWARE15.der is already enrolled and that means VMWare should be working.


