Origins of SSL and TLS:
http://tim.dierks.org/2014/05/security-standards-and-name-changes-in.html

Basically, TLS has superseded SSL. So, the `s` in `https` stands for TLS. But people use SSL/TLS interchangeably because TLS is like SSL 3.1. A minor update on SSL 3.0. And changed name.

Are SSL and TLS certificates different? No, they are the same X.509 digital certificates.

default port for TLS is 443. Browser knows that so when you request URl using `HTTPS` and don't specify port, the browser sends it to 443 by default. 


http://times.usefulinc.com/2008/06/18-cert-maint

http://times.usefulinc.com/2008/06/20-secure-ldap

How to create key and certificates for SSL ( easy, only run 4 commands on linux ) :

http://www.akadia.com/services/ssh_test_certificate.html

How to convert .crt and .key in .pem
http://stackoverflow.com/questions/991758/how-to-get-an-openssl-pem-file-from-key-and-crt-files


openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

----------------------------------------
## One-way and two-way ssl
--------------------------------------
ref:https://www.youtube.com/watch?v=ohn89zOcf4M

- one-way ssl is when only client authenticates server while server doesn't care about knowing identity of client. Like when you access google.com. Or any other bank site which is https enabled.
- two-way ssl is when both party want to know and ensure the identity of other party. This is usually when two applications talk to each other. For example, when applications use middle ware like Tibco etc


## Generating keypair -> CSR -> cert

- **Keypair** : First of all, you create a key-pair, which is a single file that holds your private and public key
  - if you want you can extract public key from this key-pair file to circulate to other parties
- **CSR** : From key pair, you generate *Certificate Signing Request* in a `.csr` file. This file is sent to certificate authority to request a sign. When you are creating CSR, it'll ask for your details like org name, location data, common name etc. Here, common name is most important input which should be the domain for which you are requesting a signed certificate.
- **Signed certificate** : Using details in CSR, and after due diligence, CA will send back a signed certificate. Or you can create your own self signed certificate. Usually with `.cer` extension. **REMEMBER**: CA only certifies your public key in form of certificate. Private key will never leave your machine. so a certificate is in short, is your public key with signature of a CA.

## Certificate storage:

#### Keystore vs Truststore

Keystore holds private key and certified public key, while truststore hold only certified public keys. In one way SSL, server will have the keystore while client will have the truststore. If certified public key of server exists in trust store of client then client can trust server's identity. 


Once you have created key-pair and signed certificate (self or CA), you need to import them into Keystore. 


#### Keystore



#### Truststore



## Steps in applying certs in a client-server Jetty app

##### server:

- create keypair
- create self signed cert
- add these to your server keystore
- give cert to client app

##### client

- export root, intermediate and publickey cert on your machine
- now import these certs ( root first, the intermediate and then public key) in trust store. 
- load ( or point your application ) to this truststore.
- then make call to server


### IMP commands to work with java keystore or truststore

#### see what is in the keystore
```
keytool -list -keystore keystore.test.local.jans.io.jks
```

## SSL key Vs SSH key

#### what are they and when they are used?
- SSL key: used to send encrypted messages to owner of the private key. Owner of the private key will share the public key with the other party(message sender). Then sender will encrypt a file using public key and then send across to the owner of the private key. Owner of the private key can decrypt. Tool used to create private and public key pair is `openssl`
- SSH key: used to authenticate SSH session with remote machine. Here, the person needing ssh access to a machine will give a public key to administrator of the server. The admin will add that public key to the target server. Once after this configuration, when the person tries to access the machine using ssh, the protocol will look at private keys stored under `~/.ssh/` folder to authenticate. Since public key is already there on the server, it will be successful. Tool that is used for generating ssh key is `ssh-keygen`. By default, your ssh keys are generated under `~/.ssh/` directory

#### how are they generated?
- SSL
  - generating private key: `openssl genrsa -aes128 -out ~/my-ssl-keys/my-ssl.pem 1024`
  - getting public key: `openssl rsa -in ~/my-ssl-keys/my-ssl.pem -pubout > /tmp/my_public_key-temp.pem`
  - See the public key: `cat /tmp/my_public_key-temp.pem`
- SSH
  - generating private key: `ssh-keygen -o`
  - getting corresponding public key: `ssh-keygen -y -f private-key-path > my-ssh-pub-key.pub`

#### Steps involved in getting ssh access to a server from admin:
- Give your **SSH** public key to admin
- he adds your key to the server
- You use the command `ssh -p 22222 -i path-to-private-key root@www.gluu.org`

#### How admin can share user id password of something in encrypted format with you
- Give your **SSL** public key to admin
- admin will put username and password in a text file
- He will use your public key to encrypt that text file
- Send you encrypted text file via chat or email etc
- You use this command to decrypt the content: `openssl rsautl -decrypt -inkey path-to-private-key -in path-to-encrypted-file > path-to-output-file` like `openssl rsautl -decrypt -inkey ~/my-ssl-keys/my-ssl.pem -in ~/docs/office/gluu/gluu_password_for_gluu_org.enc > gluu_password_for_gluu_org.txt`

## SSH

### Create a keypair

To create a `ed25519` key (sites like github and gitlab suggest and accept these keys)

```
ssh-keygen -t ed25519 -C "my-generic-key"
```

To create an rsa key

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Key pair gets created under `~/.ssh/` directory in form of two files with same name. One of them has `.pub` extension as it contains public key.

To see and copy the public key (so that you can provide it to github/gitlab etc). Just open the `.pub` file with `vim` and copy the content.
