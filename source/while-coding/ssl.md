http://times.usefulinc.com/2008/06/18-cert-maint

http://times.usefulinc.com/2008/06/20-secure-ldap

How to create key and certificates for SSL ( easy, only run 4 commands on linux ) :

http://www.akadia.com/services/ssh_test_certificate.html

How to convert .crt and .key in .pem
http://stackoverflow.com/questions/991758/how-to-get-an-openssl-pem-file-from-key-and-crt-files


openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt


