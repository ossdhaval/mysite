# Apache2 on Ubuntu

### Good reference
basics: https://phoenixnap.com/kb/how-to-install-apache-web-server-on-ubuntu-18-04#:~:text=They%20are%20all%20located%20in,Apache%20does%20on%20your%20system.

ssl : https://www.arubacloud.com/tutorial/how-to-enable-https-protocol-with-apache-2-on-ubuntu-20-04.aspx

enable sso:
only enabled modules as per ssl links.
no changes in the certificates.
no changes in the port configurations
added `ServerName test.local.rp.io` in `/etc/apache2/sites-available/default-ssl.conf`
