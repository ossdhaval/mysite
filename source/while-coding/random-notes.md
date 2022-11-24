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
sudo openssl req -new -x509 -newkey rsa:2048 -keyout VMWARE15.priv -outform DER -out VMWARE15.der -nodes -days 36500 -subj "/CN=VMWARE/"
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


## Encryption Vs Hashing

Ref:
- https://www.ssl2buy.com/wiki/difference-between-hashing-and-encryption#:~:text=The%20difference%20between%20hashing%20and%20encryption&text=In%20short%2C%20encryption%20is%20a,but%20also%20have%20some%20similarities.
- https://www.simplilearn.com/tutorials/cyber-security-tutorial/sha-256-algorithm#:~:text=It%20takes%20a%20piece%20of,called%20the%20hash%20value%2Fdigest.

Hashing and Encryption have different functions. Encryption includes encryption and decryption process while hashing is a one-way process that derives a message digest (alphnumeric string ) from data. This string is irreversible meaning you can't derive data back from string. 

**Hashing algorithms:**

SHA algorithm – **S**ecure **H**ash **A**lgorithm was designed by the National Security Agency to be used in their digital signature algorithm. It has a length of 160 bits. Just like the latter, security weaknesses in it means that it is no longer used SHA and SHA-1, organizations are using strong SHA-2 (256 bit) algorithm for the cryptographic purpose. 

**Usages:**

- systems store password in hashed format. Meaning to confirm password is correct or not they derive SHA256 hash from it and compare the hash. For same password, everytime the has will be same.
- Check the authenticity of downloaded files. 
  - Download provider provides file and also publishes SHA256sum with it. User after download can generate SHA256sum from downloaded file and compare with what is published by the provider. If the downloaded file is tempered with, the SHA will not be the same. 

**Purpose of hashing:**

Hashing can be used to compare a large amount of data. Hash values can be created for different data, meaning that it is easier comparing hashes than the data itself.
 It is easy to find a record when the data is hashed.
Hashing algorithms are used in cryptographic applications like a digital signature.
Hashing is used to generate random strings to avoid duplication of data stored in databases.
Geometric hashing – widely used in computer graphics to find closet pairs and proximity problems in planes. It is also called grid method and it has also been adopted in telecommunications.
These characteristics mean that hash can be used to store passwords. This way, it becomes difficult for someone who has the raw data to reverse them.
