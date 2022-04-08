# Apache2 on Ubuntu

### Good reference
basics: https://phoenixnap.com/kb/how-to-install-apache-web-server-on-ubuntu-18-04#:~:text=They%20are%20all%20located%20in,Apache%20does%20on%20your%20system.

ssl : https://www.arubacloud.com/tutorial/how-to-enable-https-protocol-with-apache-2-on-ubuntu-20-04.aspx

### Install Apache
Run following commands to install Apache server.
```
sudo apt-get update
sudo apt-get install apache2
```

Run following command to see the Apache services are active
```
sudo systemctl status apache2.service
```

enable sso:
- only enabled modules as per ssl links.
- no changes in the certificates.
- no changes in the port configurations
- added `ServerName test.local.rp.io` in `/etc/apache2/sites-available/default-ssl.conf`
- also executed `Configure Your Firewall` section of [this](https://phoenixnap.com/kb/how-to-install-apache-web-server-on-ubuntu-18-04#:~:text=They%20are%20all%20located%20in,Apache%20does%20on%20your%20system.)


How to configure virtual host:
https://docs.oracle.com/en/operating-systems/oracle-linux/6/admin/ol_virthosts.html#:~:text=The%20Apache%20HTTP%20server%20supports,content%20and%20to%20behave%20differently.

### Useful commands
- `apache2ctl -M` to see which all module are active
- 
