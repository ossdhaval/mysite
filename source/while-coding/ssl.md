http://times.usefulinc.com/2008/06/18-cert-maint

http://times.usefulinc.com/2008/06/20-secure-ldap

How to create key and certificates for SSL ( easy, only run 4 commands on linux ) :

http://www.akadia.com/services/ssh_test_certificate.html

How to convert .crt and .key in .pem
http://stackoverflow.com/questions/991758/how-to-get-an-openssl-pem-file-from-key-and-crt-files


openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

----------------------------------------
One-way and two-way ssl
--------------------------------------
ref:https://www.youtube.com/watch?v=ohn89zOcf4M

- one-way ssl is when only client authenticates server while server doesn't care about knowing identity of client. Like when you access google.com. Or any other bank site which is https enabled.
- two-way ssl is when both party want to know and ensure the identity of other party. This is usually when two applications talk to each other. For example, when applications use middle ware like Tibco etc



