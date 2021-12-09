Origins of SSL and TLS:
http://tim.dierks.org/2014/05/security-standards-and-name-changes-in.html

Basically, TLS has superseded SSL. So, the `s` in `https` stands for TLS. But people use SSL/TLS interchangeably because TLS is like SSL 3.1. A minor update on SSL 3.0. And changed name.

Are SSL and TLS certificates different? No, they are the same X.509 digital certificates.


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
