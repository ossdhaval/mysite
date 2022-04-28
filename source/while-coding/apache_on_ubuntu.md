# Apache2 on Ubuntu

### Good reference
basics: https://phoenixnap.com/kb/how-to-install-apache-web-server-on-ubuntu-18-04#:~:text=They%20are%20all%20located%20in,Apache%20does%20on%20your%20system.
Configuration file details: https://httpd.apache.org/docs/2.4/sections.html


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

Enable sso:
From the link: https://www.arubacloud.com/tutorial/how-to-enable-https-protocol-with-apache-2-on-ubuntu-20-04.aspx
- Perform step `Configuring the Apache SSL parameters` section
- Enabled modules as per `How to configure Apache` section 
- no changes in the certificates.
- no changes in the port configurations
- added `ServerName test.local.rp.io` in `/etc/apache2/sites-available/default-ssl.conf`
- Firewall on Ubuntu was inactive by default so did not have to configure it. But if you have an active firewall then execute `Configure Your Firewall` section of [this](https://phoenixnap.com/kb/how-to-install-apache-web-server-on-ubuntu-18-04#:~:text=They%20are%20all%20located%20in,Apache%20does%20on%20your%20system.)


How to configure virtual host:
https://docs.oracle.com/en/operating-systems/oracle-linux/6/admin/ol_virthosts.html#:~:text=The%20Apache%20HTTP%20server%20supports,content%20and%20to%20behave%20differently.

### Useful commands
- `apache2ctl -M` to see which all module are active

### logging
- apache logs can be found at `/var/log/apache2`
  - Under this you'll find files like `access.log` and `error.log`. As name suggests access log will log every request and response ([more](https://www.sumologic.com/blog/apache-access-log/#:~:text=What%20are%20Apache%20Access%20Logs,processed%20by%20the%20Apache%20server.)), while error will give you errors.
- You can configure logging level under apache configuration file `sudo vim /etc/apache2/apache2.conf`. After this restart apache2 using `systemctl restart apache2`.
- `error.log` file is misnamed by apache because it doesn't just pring errors. It follows the leve set in `LogLevel` directive. For example `LogLevel info` will print all the info. By default it is set to warn.
- If log level is warn then it'll not print problems like 404. You have to set level to info for that. 
- You can set log level for just one module also, like `LogLevel warn core:info`. This will print info level for `core` module but keep `warn` for all other. 
- useful logging links
  - https://httpd.apache.org/docs/2.4/logs.html
  - https://stackoverflow.com/questions/20386073/apache-httpd-request-response-logging
