### Installing Janssen on a machine with static IP ( in my case GCP with static IP )

1) `cd ~`
2) `wget https://raw.githubusercontent.com/JanssenProject/jans-setup/master/install.py > install.py`
3) `sudo python3 install.py.1"` or if you want to load test data too then `sudo python3 install.py.1 --args="-t"`

Sample output:

```

dhaval@test:~$ sudo python3 install.py.1 --args="-t"
Downloading https://github.com/JanssenProject/jans-setup/archive/master.zip to /opt/dist/jans/jans-setup.zip
Downloading https://corretto.aws/downloads/resources/11.0.8.10.1/amazon-corretto-11.0.8.10.1-linux-x64.tar.gz to /opt/dist/app/amazon-corretto-11.0.8.10.1-linux-x64.tar.gz
Downloading https://repo1.maven.org/maven2/org/eclipse/jetty/jetty-distribution/9.4.31.v20200723/jetty-distribution-9.4.31.v20200723.tar.gz to /opt/dist/app/jetty-distribution-9.4.31.v20200723.tar.gz
Downloading https://repo1.maven.org/maven2/org/python/jython-installer/2.7.2/jython-installer-2.7.2.jar to /opt/dist/app/jython-installer-2.7.2.jar
Downloading https://ox.gluu.org/maven/org/gluufederation/opendj/opendj-server-legacy/4.4.10/opendj-server-legacy-4.4.10.zip to /opt/dist/app/opendj-server-legacy-4.4.10.zip
Downloading https://maven.jans.io/maven/io/jans/jans-auth-server/1.0.0-SNAPSHOT/jans-auth-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-auth.war
Downloading https://maven.jans.io/maven/io/jans/jans-auth-client/1.0.0-SNAPSHOT/jans-auth-client-1.0.0-SNAPSHOT-jar-with-dependencies.jar to /opt/dist/jans/jans-auth-client-jar-with-dependencies.jar
Downloading https://maven.jans.io/maven/io/jans/jans-config-api/1.0.0-SNAPSHOT/jans-config-api-1.0.0-SNAPSHOT-runner.jar to /opt/dist/jans/jans-config-api-runner.jar
Downloading https://maven.jans.io/maven/io/jans/jans-fido2-server/1.0.0-SNAPSHOT/jans-fido2-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-fido2.war
Downloading https://maven.jans.io/maven/io/jans/jans-scim-server/1.0.0-SNAPSHOT/jans-scim-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-scim.war
Downloading https://jenkins.jans.io/maven/io/jans/jans-eleven-server/1.0.0-SNAPSHOT/jans-eleven-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-eleven.war
Downloading https://api.github.com/repos/JanssenProject/jans-cli/tarball/main to /opt/dist/jans/jans-cli.tgz
Downloading https://github.com/sqlalchemy/sqlalchemy/archive/rel_1_3_23.zip to /opt/dist/jans/sqlalchemy.zip
Downloading https://www.apple.com/certificateauthority/Apple_WebAuthn_Root_CA.pem to /opt/dist/app/Apple_WebAuthn_Root_CA.pem
Extracting jans-setup package
Downloading https://raw.githubusercontent.com/JanssenProject/jans-config-api/jans-config-api-33/docs/jans-config-api-swagger.yaml to /opt/jans/jans-setup/setup_app/data/jans-config-api-swagger.yaml
Downloading https://raw.githubusercontent.com/JanssenProject/jans-scim/master/server/src/main/resources/jans-scim-openapi.yaml to /opt/jans/jans-setup/setup_app/data/jans-scim-openapi.yaml
Launching Janssen Setup
Warning: Available free disk space was determined to be 9.3 GB. This is less than the required disk space of 40 GB.
Proceed anyways? [Y|n] Y

Installing Janssen Server...

For more info see:
  /opt/jans/jans-setup/logs/setup.log  
  /opt/jans/jans-setup/logs/setup_error.log

Detected OS     :   ubuntu 20
Janssen Version :  1.0.0-SNAPSHOT
Detected init   :  systemd
Detected Apache :  2.4

Do you acknowledge that use of the Janssen Server is under the Apache-2.0 license? [N|y] : y
Enter IP Address [10.160.0.5] : 
Enter hostname [janssen-7may.asia-south1-c.c.my-project-1-309406.internal] : test.jans.gluu.org 
Enter your city or locality : ahm
Enter your state or province two letter code : gj
Enter two letter Country Code : in
Enter Organization Name : gluu org
Enter email address for support at your organization : dhaval@gluu.org
Enter maximum RAM for applications in MB [13260] : 
Enter Password for LDAP Admin (cn=directory manager) [pc9XgB] : Pwd@g1uu
Enter Password for Admin User [Pwd@g1uu] : 
Install Apache HTTPD Server [Yes] : 
Install OAuth2 Authorization Server? [Yes] : 
Install Jans Auth Config Api? [Yes] : 
Install Gluu Admin UI? [No] : Yes
Install Scim Server? [Yes] : 
Install Fido2 Server? [Yes] : 
Install Eleven Server? [No] : Yes
Checking Properties

hostname                                       test.jans.gluu.org
orgName                                                  gluu org
os                                                         ubuntu
city                                                          ahm
state                                                          gj
countryCode                                                    in
Applications max ram (MB)                                   10608
OpenDJ max ram (MB)                                          2652
Backends                                                   opendj
Java Type                                                     jre
Install Apache 2 web server                                  True
Install Auth Server                                          True
Install Jans Auth Config Api                                 True
Install Gluu Admin UI                                        True
Install Fido2 Server                                         True
Install Scim Server                                          True
Install Eleven Server                                        True

Proceed with these values [Y|n] Y


 
Janssen Server installation successful!
CLI available to manage Jannsen Server:
/opt/jans/jans-cli/config-cli.py
/opt/jans/jans-cli/scim-cli.py

 
✓ jans             Calculating application memory
✓ jre              Installing Jre
✓ jetty            Installing Jetty
✓ jython           Installing Jython
✓ opendj           OpenDJ post installation
✓ apache2          Configuring apache2
✓ jans-auth        Generating OAuth openid keys
✓ jans-config-api  Installing Jans-Config-Api
✓ jans-fido2       Installing Jans-Fido2
✓ jans-scim        Installing Jans-Scim
✓ jans-eleven      Installing softhsm
✓ jans-cli         Installing Jans Cli
✓ gluu-admin-ui    Installing Gluu-Admin-Ui
✓ test-data        Updating schema
✓ post-setup       Starting Gluu Admin Ui

dhaval@test:~$ 

```
