# Janssen Notes

Note : many times docs mention that run this command from 'Inside the Gluu Server chroot', or 'run it from gluu container' etc. All this means one thing that you first login to the gluu container using

/sbin/gluu-serverd login
and then run commands.


==================================

 Janssen local install installation instructions :

===================================

https://github.com/JanssenProject/jans-setup

```

cd ~

dhaval@dhaval-Lenovo-U41-70:~$ curl https://raw.githubusercontent.com/JanssenProject/jans/main/jans-linux-setup/install.py > install.py

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current

                                 Dload  Upload   Total   Spent    Left  Speed

100  8911  100  8911    0     0  16876      0 --:--:-- --:--:-- --:--:-- 16876





dhaval@dhaval-Lenovo-U41-70:~$ sudo python3 install.py or if you want to install with test data then sudo python3 install.py --args="-t"

[sudo] password for dhaval: 
Downloading https://github.com/JanssenProject/jans-setup/archive/master.zip to /opt/dist/jans/jans-setup.zip
Downloading https://corretto.aws/downloads/resources/11.0.8.10.1/amazon-corretto-11.0.8.10.1-linux-x64.tar.gz to /opt/dist/app/amazon-corretto-11.0.8.10.1-linux-x64.tar.gz
Downloading https://repo1.maven.org/maven2/org/eclipse/jetty/jetty-distribution/9.4.31.v20200723/jetty-distribution-9.4.31.v20200723.tar.gz to /opt/dist/app/jetty-distribution-9.4.31.v20200723.tar.gz
Downloading https://repo1.maven.org/maven2/org/python/jython-installer/2.7.2/jython-installer-2.7.2.jar to /opt/dist/app/jython-installer-2.7.2.jar
Downloading https://ox.gluu.org/maven/org/gluufederation/opendj/opendj-server-legacy/4.0.0.gluu/opendj-server-legacy-4.0.0.gluu.zip to /opt/dist/app/opendj-server-legacy-4.0.0.gluu.zip
Downloading https://maven.jans.io/maven/io/jans/jans-auth-server/1.0.0-SNAPSHOT/jans-auth-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-auth.war
Downloading https://maven.jans.io/maven/io/jans/jans-auth-client/1.0.0-SNAPSHOT/jans-auth-client-1.0.0-SNAPSHOT-jar-with-dependencies.jar to /opt/dist/jans/jans-auth-client-jar-with-dependencies.jar
Downloading https://maven.jans.io/maven/io/jans/jans-config-api/1.0.0-SNAPSHOT/jans-config-api-1.0.0-SNAPSHOT-runner.jar to /opt/dist/jans/jans-config-api-runner.jar
Downloading https://maven.jans.io/maven/io/jans/jans-fido2-server/1.0.0-SNAPSHOT/jans-fido2-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-fido2.war
Downloading https://maven.jans.io/maven/io/jans/jans-scim-server/1.0.0-SNAPSHOT/jans-scim-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-scim.war
Downloading https://jenkins.jans.io/maven/io/jans/jans-eleven-server/1.0.0-SNAPSHOT/jans-eleven-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-eleven.war
Downloading https://api.github.com/repos/JanssenProject/jans-cli/tarball/main to /opt/dist/jans/jans-cli.tgz
Downloading https://github.com/sqlalchemy/sqlalchemy/archive/rel_1_3_23.zip to /opt/dist/jans/sqlalchemy.zip
Extracting jans-setup package
Downloading https://raw.githubusercontent.com/JanssenProject/jans-config-api/master/docs/jans-config-api-swagger.yaml to /opt/jans/jans-setup/setup_app/data/jans-config-api-swagger.yaml
Downloading https://raw.githubusercontent.com/JanssenProject/jans-scim/master/server/src/main/resources/jans-scim-openapi.yaml to /opt/jans/jans-setup/setup_app/data/jans-scim-openapi.yaml
Launching Janssen Setup
The following packages are required for Janssen Server
apache2 python3-ldap3 python3-ruamel.yaml python3-pymysql
Do you want to install these now? [Y/n] y  
Installing packages apache2 python3-ldap3 python3-ruamel.yaml python3-pymysql

Installing Janssen Server...

For more info see:
  /opt/jans/jans-setup/logs/setup.log  
  /opt/jans/jans-setup/logs/setup_error.log

Detected OS     :   ubuntu 20
Janssen Version :  1.0.0-SNAPSHOT
Detected init   :  systemd
Detected Apache :  2.4

Do you acknowledge that use of the Janssen Server is under the Apache-2.0 license? [N|y] : y
Enter IP Address [192.168.1.6] : 
Enter hostname [dhaval-Lenovo-U41-70] : localhost
Hostname can't be localhost
Enter hostname [dhaval-Lenovo-U41-70] : dd-lenovo
Enter your city or locality : Ahm
Enter your state or province two letter code : gj
Enter two letter Country Code : in
Enter Organization Name : myorg
Enter email address for support at your organization : support@myorg.org
Enter maximum RAM for applications in MB [6545] : 2000
Enter Password for LDAP Admin (cn=directory manager) [z7hmG8] : myldapadmin
Enter Password for Admin User [myldapadmin] : myadmin
Install Apache HTTPD Server [Yes] : y
Install OAuth2 Authorization Server? [Yes] : y
Install Jans Auth Config Api? [Yes] : y
Install Scim Server? [Yes] : y
Install Fido2 Server? [Yes] : y
Install Eleven Server? [No] : y

hostname                                                dd-lenovo
orgName                                                     myorg
os                                                         ubuntu
city                                                          Ahm
state                                                          gj
countryCode                                                    in
Applications max ram (MB)                                    1600
OpenDJ max ram (MB)                                           400
Backends                                                   opendj
Java Type                                                     jre
Install Apache 2 web server                                  True
Install Auth Server                                          True
Install Jans Auth Config Api                                 True
Install Fido2 Server                                         True
Install Scim Server                                          True
Install Eleven Server                                        True

Proceed with these values [Y|n] y
✓ jans             Calculating application memory
                                                 ✓ jre              Installing Jre
                                                                                  ✓ jetty            Installing Jetty
                              ✓ jans             Calculating application memory
                                                                               ✓ jre              Installing Jre
                                                                                                                ✓ jetty            Installing Jetty
                                                            ✓ jans             Calculating application memory
                                                                                                             ✓ jre              Installing Jre
                                                                                                                                              ✓ jetty                                                                                           ✓ jans             Calculating application memory
                                                                                                                                           ✓ jre              Installing Jre
                                                                                                                        ✓ jans             Calculating application memory
                   ✓ jre              Installing Jre
                                                                                                                                                     ✓ jans             Calculating application memory
                                                ✓ jre              Installing Jre
                                                                                 ✓ jetty            Installing Jetty
                             ✓ jans             Calculating application memory
                                                                              ✓ jre              Installing Jre
                                                                                                               ✓ jetty            Installing Jetty
                                                           ✓ jans             Calculating application memory
                                                                                                            ✓ jre              Installing Jre
                                                                                                                                             ✓ jetty                                                                                           ✓ jans             Calculating application memory
                                                                                                                                          ✓ jre              Installing Jre
                                                                                                                       ✓ jans             Calculating application memory
                  ✓ jre              Installing Jre
                                                                                                                                                     ✓ jans             Calculating 
 
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
✓ post-setup       Starting Jans Eleven

```

```

dhaval@dhaval-Lenovo-U41-70:~$ 


python3 install.py

sudo python3 install.py



questions and responses : 

--------------------------------

Do you acknowledge that use of the Janssen Server is under the Apache-2.0 license? [N|y] : y

Enter IP Address [192.168.1.6] : 

Enter hostname [dhaval-Lenovo-U41-70] : localhost

Hostname can't be localhost

Enter hostname [dhaval-Lenovo-U41-70] : dd-lenovo

Enter your city or locality : Ahm

Enter your state or province two letter code : gj

Enter two letter Country Code : in

Enter Organization Name : myorg

Enter email address for support at your organization : support@myorg.org

Enter maximum RAM for applications in MB [6545] : 2000

Enter Password for LDAP Admin (cn=directory manager) [z7hmG8] : myldapadmin

Enter Password for Admin User [myldapadmin] : myadmin

Install Apache HTTPD Server [Yes] : y

Install OAuth2 Authorization Server? [Yes] : y

Install Jans Auth Config Api? [Yes] : y

Install Scim Server? [Yes] : y

Install Fido2 Server? [Yes] : y

Install Eleven Server? [No] : y



hostname                                                dd-lenovo

orgName                                                     myorg

os                                                         ubuntu

city                                                          Ahm

state                                                          gj

countryCode                                                    in

Applications max ram (MB)                                    1600

OpenDJ max ram (MB)                                           400

Backends                                                   opendj

Java Type                                                     jre

Install Apache 2 web server                                  True

Install Auth Server                                          True

Install Jans Auth Config Api                                 True

Install Fido2 Server                                         True

Install Scim Server                                          True

Install Eleven Server                                        True



Proceed with these values [Y|n] Y



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

post-setup       Starting Jans Scim



Post setup will start all the components one by one



Janssen Server installation successful!

CLI available to manage Jannsen Server:

/opt/jans/jans-cli/config-cli.py

/opt/jans/jans-cli/scim-cli.py

```



Uninstall

----------

```

dhaval@dd-lenovo:~$ sudo python3 install.py -uninstall
[sudo] password for dhaval: 

This process is irreversible.
You will lose all data related to Janssen Server.


 
Are you sure to uninstall Janssen Server? [yes/N] yes

Uninstalling Jannsen Server...
Stopping OpenDj Server
Server already stopped
Removing /etc/default/jans-auth
Stopping jans-auth
Removing /etc/default/jans-fido2
Stopping jans-fido2
Removing /etc/default/jans-scim
Stopping jans-scim
Removing /etc/default/jans-eleven
Stopping jans-eleven
Executing rm -r -f /etc/certs
Executing rm -r -f /etc/jans
Executing rm -r -f /opt/jans
Executing rm -r -f /opt/amazon-corretto*
Executing rm -r -f /opt/jre
Executing rm -r -f /opt/jetty*
Executing rm -r -f /opt/jython*
Executing rm -r -f /opt/opendj
Executing rm -r -f /opt/dist
dhaval@dd-lenovo:~$

```

==================================

 Janssen local install using lxd instructions :

===================================

```

snap install lxd

snap refresh

lxd init # Default settings looks good. I only specified 'dir' (question 4) storage method to access container filesystem /var/snap/lxd/common/lxd/storage-pools/default/containers/ubuntu20/rootfs/

lxc launch images:ubuntu/20.04/amd64 ubuntu20

lxc config device add ubuntu20 myport443 proxy listen=tcp:0.0.0.0:443 connect=tcp:127.0.0.1:443

lxc config device add ubuntu20 myport1636 proxy listen=tcp:0.0.0.0:1636 connect=tcp:127.0.0.1:1636

lxc config set ubuntu20 limits.memory 4GB

lxc exec ubuntu20 -- sudo --user root --login

apt install curl

curl https://raw.githubusercontent.com/JanssenProject/jans/main/jans-linux-setup/install.py > install.py

python3 install.py
after this, following questionnaire will come uup:
Do you acknowledge that use of the Janssen Server is under the Apache-2.0 license? [N|y] : y
Enter IP Address [10.203.235.5] : 
Enter hostname [ubuntu20.lxd] : 
Enter your city or locality : ah
Enter your state or province two letter code : gj
Enter two letter Country Code : in
Enter Organization Name : gluu inc.
Enter email address for support at your organization : dhaval@gluu.org
Enter maximum RAM for applications in MB [6545] : 
Enter Password for LDAP Admin (cn=directory manager) [WCZy19] : Pwd@g1uu
Enter Password for Admin User [Pwd@g1uu] : 
Install Apache HTTPD Server [Yes] : 
Install OAuth2 Authorization Server? [Yes] : 
Install Jans Auth Config Api? [Yes] : 
Install Scim Server? [Yes] : 
Install Fido2 Server? [Yes] : 
Install Eleven Server? [No] : Yes

hostname                                             ubuntu20.lxd
orgName                                                 gluu inc.
os                                                         ubuntu
city                                                           ah
state                                                          gj
countryCode                                                    in
Applications max ram (MB)                                    5236
OpenDJ max ram (MB)                                          1309
Backends                                                   opendj
Java Type                                                     jre
Install Apache 2 web server                                  True
Install Auth Server                                          True
Install Jans Auth Config Api                                 True
Install Fido2 Server                                         True
Install Scim Server                                          True
Install Eleven Server                                        True

```

======================================= 
installing gluu server on GCP from https://www.youtube.com/watch?v=0RskrQG8km8&t=99s
( but this installs 4.1 )
==================================



===================================================
installing gluu gateway on GCP VM 
===================================================
create a E2 instance ( 1 cpu, 2gb ram, 10 gb hdd, enable https, boot 
image = ubuntu 18 )

Open browser shell from GCP dashboard 'ssh' dropdown
sudo su
start following 
https://gluu.org/docs/gg/4.1/installation/#install-the-gluu-gateway-package

===================================
install gluu server 4.2 on GCP
(https://gluu.org/docs/gluu-server/4.2/installation-guide/install-ubuntu/)
===================================
Remember that though we are installing on GCP, it is not 'cloud' install like
GKE. Instead of local VM, we are having VM on GCP, that is the only difference.
So, we are not following installation guide for cloud native but simple Ubuntu install.

For vm preparation : 
-----------------------
useful video at : https://www.youtube.com/watch?v=0RskrQG8km8&t=99s
but use this just for understanding purpose, for exact values to be used, refer 
to details below :
Create a new GCP vm with values below :
name: anything ( gluu-server-4-2 )
machine family : E2
type : E2-medium ( 2 cpu, 4 gb ram or 8 gb )

Boot disk : OS(Ubuntu), version (20.04 LTS), disk ( balanced persistence ), 
size (50 gb)

firewall : select 'allow HTTPS traffic'
--1,2,3 are optional. Required only if you want to access 
1) click on 'Management, security, disks, networking, sole tenancy'
2) under 'security', check 'Block project-wide SSH keys'
3) create public key on your local machine from where you need ssh access to GCP vm
and paste public key in 'enter public key' text area
Note on how to get public key :
cd ~/.ssh
cat id_dsa.pub ( if this file exists then copy the content from it and paste it in the GCP text area)
if this file doesn't exist then run command 'ssh-keygen -o' to generate this file and copy the content from it to GCP text area)

When you paste public key in the 'enter public key' area, GCP will auto detect user
name from public key and display it on the left of the text area. 
This is your username when trying to ssh connection from your local pc to GCP vm. 
So, make note of this name. 
( if you don't want to do ssh setup and all, you can skip 1,2,3 above and instead
directly click 'create'. Once your VM is ready, on the GCP 'VM instance' dashboard, 
you can click on drop-down under 'connect' column, and select 
'open in browser window'. This will give you a in-browser commandline client.)

click 'create'
Once your VM is creaeted and if you have done ssh setup like in above 1,2,3, then you
can connect to your vm from your local machine using command below :
ssh -i ~/.ssh/id_rsa dhaval@34.123.24.4
here 'dhaval' is username that we noted in 3 above, and IP is 'external ip' 
as mentioned on gcp 'vm instances' dashboard.

make external IP as permanent : at this point, the external IP assinged to your VM is
ephemeral. It'll change everytime when you restart your instance. To avoid this,
On dashboard search for 'vpc network' and to into that section
click 'external IP addresses'
change type of your IP to 'static' from ephemeral

---- now install gluu server 4.2 
(reference : https://gluu.org/docs/gluu-server/4.2/installation-guide/install-ubuntu/)
connect to your VM via ssh.

```
sudo su
echo "deb https://repo.gluu.org/ubuntu/ focal main" > /etc/apt/sources.list.d/gluu-repo.list
curl https://repo.gluu.org/ubuntu/gluu-apt.key | apt-key add -
apt update
apt install gluu-server
apt-mark hold gluu-server
---- now start the server
/sbin/gluu-serverd enable
/sbin/gluu-serverd start
/sbin/gluu-serverd login
---- start initial setup
cd /install/community-edition-setup
./setup.py
Fill out prompts as per below :
root@localhost:/install/community-edition-setup# ./setup.py
Detected OS ubuntu 20
Warning: Available free disk space was determined to be 34.7 GB. This is less than the required disk space of 40 GB.
Proceed anyways? [Y|n] y

Installing Gluu Server...
Detected OS  :  ubuntu
Detected init:  systemd
Detected Apache:  2.4

Installing Gluu Server...

For more info see:
  /install/community-edition-setup/setup.log  
  /install/community-edition-setup/setup_error.log

Do you acknowledge that use of the Gluu Server is under the Apache-2.0 license? [N|y] : y
Enter IP Address [10.128.0.4] : 
Enter hostname [gluu-server-4-2.us-central1-a.c.xenon-pager-308802.internal] : gluuserver.gluu.org
Enter your city or locality : ah
Enter your state or province two letter code : gj
Enter two letter Country Code : in
Enter Organization Name : Gluu Inc
Enter email address for support at your organization : dhaval@gluu.org
Enter maximum RAM for applications in MB [3432] : 
Enter oxTrust Admin Password [t1Wi&hUdXwvm] : 
Enter Password for LDAP Admin (cn=directory manager) [t1Wi&hUdXwvm] : 
Install oxAuth OAuth2 Authorization Server? [Yes] : 
Install oxTrust Admin UI? [Yes] : 
Install Apache HTTPD Server [Yes] : 
Install Scim Server? [No] : Yes
Install Fido2 Server? [No] : Yes
Install Shibboleth SAML IDP? [No] : Yes
Install oxAuth RP? [No] : Yes
Install Passport? [No] : Yes
Install Casa? [No] : Yes
Please enter URL of oxd-server if you have one, for example: https://oxd.mygluu.org:8443
Else leave blank to install oxd server locally.
oxd Server URL: 
  Use Authorization Server's native persistence for oxd? [No] : 
Install Gluu Radius? [No] : Yes

hostname                                      gluuserver.gluu.org
orgName                                                  Gluu Inc
os                                                         ubuntu
city                                                           ah
state                                                          gj
countryCode                                                    in
Applications max ram                                         3432
Install oxAuth                                               True
Install oxTrust                                              True
Backends                                                   opendj
Java Type                                                     jre
Install Apache 2 web server                                  True
Install Fido2 Server                                         True
Install Scim Server                                          True
Install Shibboleth SAML IDP                                  True
Install oxAuth RP                                            True
Install Passport                                             True
Install Casa                                                 True
Install Oxd                                                  True
Install Gluu Radius                                          True

if all the components have been installed successfully, then you'll see below message:

Installing [#################################] Completed                  

Encrypted properties file saved to /install/community-edition-setup/setup.properties.last.enc with password t1Wi&hUdXwvm
Decrypt the file with the following command if you want to re-use:
openssl enc -d -aes-256-cbc -in setup.properties.last.enc -out setup.properties


 Gluu Server installation successful! Point your browser to https://gluuserver.gluu.org

```

Now, before you acan access UI from you local machine, you have to make 
following entry in hosts file of your OS ( for ubuntu : /etc/hosts )
sudo vim /etc/hosts
make an entry like : 
10.128.0.4      gluuserver.gluu.org
Here, IP is external IP as mentioned in the 'vm dashboard' of gcp, 
while gluuserver.gluu.org is host name that you have given during setup script execution.
Once this is done, you can access gluu server at 
https://gluuserver.gluu.org
with user: admin
and password as mentioned during the setup prompts. In this case 't1Wi&hUdXwvm'.



===========================
handy gluu commands
===========================
https://gluu.org/docs/gluu-server/4.2/operation/services/
systemctl status [service name]
systemctl start [service name]
systemctl stop [service name]
systemctl restart [service name]

eg. : systemctl restart oxd-server

==============================
Configure oxd in GCP :
==============================
from : https://gluu.org/docs/oxd/install/#oxd-server-installation
and 
https://gluu.org/docs/oxd/configuration/oxd-configuration/

after you have installed oxd during installation of gluu server, there are 
following steps that you have to take in order to use oxd.
first ensure that oxtrust UI is accessible:
https://gluuserver.gluu.org/

Now, Before we start oxd configuration, if you try to access oxd healthcheck url, 
it won't be working.
https://gluuserver.gluu.org:8443/health-check

oxd configuration has following steps :
1) configure your public IP in oxd conf (/opt/oxd-server/conf/oxd-server.yml)
2) configure GCP firewall to allow traffic from 8443
( if whole gluu server is install on development machine then you don't need this )
3) configure certificates (couldn't successfully do this.)
( if whole gluu server is install on development machine then you don't need this )

1) configure IP as mentioned in bind_ip_addresses section of 
https://gluu.org/docs/oxd/configuration/oxd-configuration/#server-configuration-fields-descriptions
if you are going to mention IP of your local system then your external IP needs
to be mentioned. Which you can find by 'curl ifconfig.me' on Ubuntu command prompt. But 
I suggest you don't use your external IP in oxd config file as external ip may change
everytime you restart your local system. Better use ['*'].

Now restart oxd service using :
systemctl restart oxd-server

Now we need to configure GCP firewall to allow traffic on port 8443.
Go to your gcp dashboard of your project -> search 'firewall' -> open the firewall 
named 'default-allow-https' and edit it to add 8443 in the port list as below.



now if you try the health check url, you'll get response as below :
{
   "application": "oxd",
   "version": "4.2.3.Final",
   "status": "running"
}

3) I couldn't successfully execute the third step of configuring letsencrypt certificates. This is due to the fact that in order to get a letsencrypt. but if whole gluu server is install on development machine then you don't need to do this.

at this point you below endpoints should be working in your setup :
https://test.gcp.gluu.org/identity/home.htm
https://test.gcp.gluu.org:8443/health-check
https://test.gcp.gluu.org/.well-known/openid-configuration
https://test.gcp.gluu.org/.well-known/scim-configuration (if you have install scim)

also if you are running oxd demo spring app locally, it should also return 'hello' page with oxd id on below url (port as you configurd)
https://localhost:8083/
Now start oxd configuration (reference : https://gluu.org/docs/oxd/configuration/oxd-configuration/) :
In the Gluu shell : goto /opt/oxd-server/conf/oxd-server.yml
and set below properties. Customise values as per your setup:
op_configuration_endpoint: 'https://test.gcp.gluu.org/.well-known/openid-configuration'

---- run the spring oxd app :
get it from git and change following properties in application.properties
server.port=8083
oxd.server.op-host=https://test.gcp.gluu.org
oxd.server.host=test.gcp.gluu.org
oxd.client.callback-uri=https://localhost:8083/gluu/callback
oxd.client.post-logout-uri=https://localhost:8083/gluu/logout


Uninstallation

For Ubuntu Server 20.x and Ubuntu Server 18.04.x, run the following commands:

/sbin/gluu-serverd disable

/sbin/gluu-serverd stop

apt remove gluu-server

rm -fr /opt/gluu-server.save

==============================
troubleshooting
==============================

------------
getting 503 when trying to access oxtrust of a gluu server newly installed on
a kvm ( 2cpu, 4gb ). Just bare minimum server was installed with identity and 
oxauth
------------------

from host root :
checked

it was found to be active-running.
then entered gluu shell and from there check individual service status
systemctl status oxauth
systemctl status identity
both returned with 'jetty not running' status.
then went to start individual service manually so that I can debug the failure
better. For that,
/opt/dist/scripts/oxauth start
to see all the parameters being passed
/opt/dist/scripts/oxauth status

----------
getting 

`10:41:56.874 [TestNG-tests-4] ERROR io.jans.as.client.RegisterClient - PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target`

After installing fresh GCP janssen installation and then running jans-auth-server tests against it from same GCP machine.

Fix: couldn't find a root-cause but it only started working when I unintalled and reinstalled Janssen. Plus, when I was reinstalling via ssh session, GCP logged me in as `dhaval@test` while earlier it was with machine name `dhaval@21stJan`. Either the reinstallation or change in the login could have solved it. My guess is reinstall solved it.

----------
getting `package sun.security.x509 does not exist` when trying to run few Janssen test cases from Intellij like `RegistrationRestWebServiceHttpTest.requestClientAssociate1`

Fix: disable `Use --release option` from Java compiler settings in Intellij. [Reference](https://stackoverflow.com/questions/40448203/intellij-says-the-package-does-not-exist-but-i-can-access-the-package)

---------
`problem:`

Remote debugger was not able to connect to jans server on GCP. This was due to 
jans-auth service was not able to start and was getting stuck at below log message in jans-auth.log.

```
2021-06-29 06:20:08,601 INFO  [main] [jans.as.server.model.config.ConfigurationFactory] (ConfigurationFactory.java:395) - Loading configuration from 'ldap' DB...
```

`solution:` GCP instance restart worked. root cause was that ldap services were not available even though it showed `running` in systemctl command status.

---------
getting Duplicate fragment name ERROR Jetty Maven Plugin for resteasy library.
encountered this while trying to run jans-auth-server/server using jetty:run-war for first time. I had to change POM file of server project as suggested below.
solved by: https://stackoverflow.com/questions/5802096/duplicate-fragment-name-error-jetty-maven-plugin

-------------
```
Problem
```

getting 

```
Error retreiving data

Unauthorized
b'ID Token is expired'
```
when trying to use config-cli using `sudo /opt/jans/jans-cli/config-cli.py`. This error doesn't come when you fire the command but it comes when you try to use any of the menu options and give all the inputs. 

```
root-cause
```

This happens because the token which you had received earlier via device-code authentication, has now expired. You need to request a new token but CLI doesn't give you that prompt

```
solution
```

you have to log out of cli using `x` option and reinvoke cli using same command `sudo /opt/jans/jans-cli/config-cli.py`. Now when you try to execute any option, it'll give you a device code to authenticate.

=============
enable linux GUI on GCP vm
================
Use steps as mentioned here : https://github.com/eerolat/setup-google-linux

in short, while creating linux VM : 
under `management` -> automation -> startup script text area. Paste the line below:
`   wget https://github.com/eerolat/setup-google-linux/raw/master/install.sh
   sh install.sh -u myusername mypassword`

Here use and password can be anything. Same you have to use when connecting via RDP client from your local machine like remmina.

for example:
`wget https://github.com/eerolat/setup-google-linux/raw/master/install.sh
   sh install.sh -u dhaval work`

Remember, only try to connect via UI after sometime of starting the vm. Like 10 mins. 

=============================

## general notes :

- main component in Janssen and Gluu is jans-auth-server. Same component is 
called oxauth in Gluu.
- About cache refresh ([ref](https://chat.gluu.org/group/documentation?msg=Bti5ZaBtaFv2jejtr)): 

 ```
 No cache refresh (CR) in Jans

 CR is a feature in oxTrust

 We have been talking to Shekhar about making a standalone CR project in Jans

 but it’s not top priority

 CR is an enterprise feature, mostly used to connect Active Directory servers
 ```
- Janssen provides authentication using OIDC and authorization using OAuth. When referring to Janssen in context of authentication, it can be called OP(OpenId Connect Provider), while referring to Janssen in context of authorization, it can be called AS (Authorization Server) as well. So, You can refer to Janssen as OP or AS.

- `claims` word is also used for multiple things. For Janssen Server configuration properties are also called `claims` (these are the properties that we see in response to .well-known configuration endpoint `https://jans-dynamic-ldap/jans-auth/.well-known/openid-configuration`). Better call it `server claims`. `claims` is also used in context of user. These should be called `user claims` or `user attributes` for better clarity. You can see attributes (user claims) supported by server under `claims_supported` server claim as part of response to .well-known configuration endpoint mentioned above .


======================

## LDAP/opendj/dsconfig commands :

### Connecting to ldap running locally on a jans instance:

```
sudo /opt/opendj/bin/ldapsearch -h localhost -p 1636 -D "cn=directory manager" -w "Ld@padm1n" -Z -X -b "o=jans" -s one "objectclass=*" dn
```

To get dn and other details:

```
cat /opt/jans/jans-setup/setup.properties.last | egrep 'ldapPass=|ldap_binddn=|ldap_hostname=|ldaps_port='
```

### Connecting to LDAP running in an lxc container using an apache directory studio running in local machine

- You do not have to open any port and 1636 port on lxc should be open by default
- first make sure that the ldap is running and it is accessible on 1636 from within lxc using instructions above(#connecting-to-ldap-running-locally-on-a-jans-instance)
- Now open apache directory studio and create a new connect. Fill out the first form as below (remember to remove `/` from `bind dn` value if it exists like this `cn\=directory manager`. After removal, the value should be `cn=directory manager`)
- 

![image](https://user-images.githubusercontent.com/343411/226304437-54647b9b-21ad-46ae-846b-57278b243ecf.png)

- Now click next and fill out next form as below (remember to remove `/` from `bind dn` value if it exists like this `cn\=directory manager`. After removal, the value should be `cn=directory manager`):

![image](https://user-images.githubusercontent.com/343411/226305221-eeac9050-e964-49c2-b7f8-0482240b8734.png)

- click finish and you should be able see a new connection in the listing on bottom left panel. Right click on your connection and click `open connection`. It should populate tree on the top left panel and be ready to browse.

### to see all the existing indexes on backend 'userRoot':

`/opt/opendj/bin/dsconfig list-backend-indexes --backend-name userRoot`

this will ask few question to connect with Opendj. following are the responses 
if you are running server on localhost:

```

root@test:/install/community-edition-setup# /opt/opendj/bin/dsconfig list-backend-indexes --backend-name userRoot


>>>> Specify OpenDJ LDAP connection parameters

Directory server hostname or IP address [localhost]: 

Directory server administration port number [4444]: 1636

Administrator user bind DN [cn=Directory Manager]: 

Password for user 'cn=Directory Manager': <password that you entered during installation of Janssen>



Backend Index               : index-type          : index-entry-limit : index-extensible-matching-rule : confidentiality-enabled
----------------------------:---------------------:-------------------:--------------------------------:------------------------
aci                         : presence            : 4000              : -                              : false
authzCode                   : equality            : 4000              : -                              : false
chlng                       : equality            : 4000              : -                              : false

```

reference and more commands : 
https://backstage.forgerock.com/docs/ds/5/configref/

==========================
what actually happens during janssen installation via install.py :
=========================

There are primarily two scripts, install.py and setup.py.
User trigger install.py and this script inturn calls setup.py for installation task.
On top of installation Install.py provides uninstall, upgrade like functions.
 Below are the actions that install.py and setup.py scripts
take when executed.

Install.py
When triggered this script first downloads third party software like JDK, Jython etc 
for example:
Downloading https://corretto.aws/downloads/resources/11.0.8.10.1/amazon-corretto-11.0.8.10.1-linux-x64.tar.gz to /opt/dist/app/amazon-corretto-11.0.8.10.1-linux-x64.tar.gz
Plus it also downloads Janssen artifacts from Github and maven. Artifacts like jans-setup.zip, 
for example :
Downloading https://github.com/JanssenProject/jans-setup/archive/master.zip to /opt/dist/jans/jans-setup.zip
Downloading https://maven.jans.io/maven/io/jans/jans-auth-server/1.0.0-SNAPSHOT/jans-auth-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-auth.war
Downloading https://maven.jans.io/maven/io/jans/jans-auth-client/1.0.0-SNAPSHOT/jans-auth-client-1.0.0-SNAPSHOT-jar-with-dependencies.jar to /opt/dist/jans/jans-auth-client-jar-with-dependencies.jar
Downloading https://maven.jans.io/maven/io/jans/jans-config-api/1.0.0-SNAPSHOT/jans-config-api-1.0.0-SNAPSHOT-runner.jar to /opt/dist/jans/jans-config-api-runner.jar
Downloading https://maven.jans.io/maven/io/jans/jans-fido2-server/1.0.0-SNAPSHOT/jans-fido2-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-fido2.war
Downloading https://maven.jans.io/maven/io/jans/jans-scim-server/1.0.0-SNAPSHOT/jans-scim-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-scim.war
Downloading https://jenkins.jans.io/maven/io/jans/jans-eleven-server/1.0.0-SNAPSHOT/jans-eleven-server-1.0.0-SNAPSHOT.war to /opt/dist/jans/jans-eleven.war

Please note that all Janssen artifacts are downloaded from https://maven.jans.io/maven/io/jans/

then arguments of script invocation are parsed. Here one important usage is of --args argument. If you 
want to pass any argument to setup.py which is called by install.py then you have to pass that argument
to install.py as below. For example you want to call setup.py with -t argument, then

python3 install.py --args=-t

Important Jans directories are also set in script :

jans_dir = '/opt/jans'
app_dir = '/opt/dist/app'
jans_app_dir = '/opt/dist/jans'
scripts_dir = '/opt/dist/scripts'
jetty_home = '/opt/jans/jetty'

After this it takes actions according to arguments passed, like upgrade or uninstall or install.
For installation option, install.py triggers setup.py

setup.py
------------


jar and war files for janssen modules like 
check if all third party software are already installed. Like python etc.

Running: dpkg-query -W -f='${Status}' curl 2>/dev/null | grep -c "ok installed"


Module notes :
config API :
this module uses cucumber and karate for integration testing. PujaVS is familiar with
the module and wrote these tests.

Imp links for this module :
cucumber report : https://jenkins.jans.io/jenkins/job/jans-config-api/299/cucumber-html-reports_393f3d47-d30d-3acf-a82f-41b0e41e87bb/overview-features.html
swagger : https://gluu.org/swagger-ui/?url=https://raw.githubusercontent.com/JanssenProject/jans-config-api/master/docs/jans-config-api-swagger.yaml




### Installing Janssen on a machine with static IP ( in my case GCP with static IP )

1) `cd ~`
2) `wget https://raw.githubusercontent.com/JanssenProject/jans/main/jans-linux-setup/install.py > install.py`
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

#### setup remote debugging

##### changes required on Janssen server

- Open service config file

  `vim /etc/default/jans-auth`

- add line below at the end of `JAVA_OPTIONS`

  `-Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=6001`

- then restart services

  `systemctl restart jans-auth.service`
  
- (only if you are using GCP instance as jans server) add port to firewall:
  - search for firewall on dashboard search
  - edit the firewall called `default-allow-ssh`, and add port `6001`. Save settings.
  - not sure but you may want to restart your instance once for firewall settings to take effect.

##### changes required in the machine where your workspace is:

- setup port forwarding
  
  `ssh -L 6001:localhost:6001 dhaval@test.dd.jans.io`
  
  this command will open an ssl connection with jans server. Keep the window open.
  
- In IntellijIdea, 
  - `shift+shift` -> search for `edit configuration` -> click on `+` -> `remote jvm debugging` -> then give below values
  - `host:` remote host IP or name as in `hosts` file, `port:` 6001, `use module:` give the module which is being debugged on server. 

### Request and responses to imp jans config endpoints

```
OpenID Connect Configuration
-------------------------------------------------------
REQUEST:
-------------------------------------------------------
GET /.well-known/openid-configuration HTTP/1.1 HTTP/1.1
Host: test.dd.jans.io

-------------------------------------------------------
RESPONSE:
-------------------------------------------------------
HTTP/1.1 200
Connection: Keep-Alive
Content-Length: 7774
Content-Type: application/json
Date: Wed, 07 Jul 2021 08:26:48 GMT
Keep-Alive: timeout=5, max=100
Server: Apache/2.4.41 (Ubuntu)
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type-Options: nosniff
X-Xss-Protection: 1; mode=block

{
   "request_parameter_supported":true,
   "token_revocation_endpoint":"https://test.dd.jans.io/jans-auth/restv1/revoke",
   "introspection_endpoint":"https://test.dd.jans.io/jans-auth/restv1/introspection",
   "claims_parameter_supported":true,
   "issuer":"https://test.dd.jans.io",
   "userinfo_encryption_enc_values_supported":[
      "RSA1_5",
      "RSA-OAEP",
      "A128KW",
      "A256KW"
   ],
   "id_token_encryption_enc_values_supported":[
      "A128CBC+HS256",
      "A256CBC+HS512",
      "A128GCM",
      "A256GCM"
   ],
   "authorization_endpoint":"https://test.dd.jans.io/jans-auth/restv1/authorize",
   "service_documentation":"http://jans.org/docs",
   "id_generation_endpoint":"https://test.dd.jans.io/jans-auth/restv1/id",
   "claims_supported":[
      "street_address",
      "country",
      "zoneinfo",
      "birthdate",
      "role",
      "gender",
      "formatted",
      "user_name",
      "work_phone",
      "phone_mobile_number",
      "preferred_username",
      "locale",
      "inum",
      "jansIdTknSignedRespAlg",
      "jansRedirectURI",
      "updated_at",
      "nickname",
      "member_of",
      "org_name",
      "email",
      "website",
      "email_verified",
      "jansAppType",
      "profile",
      "locality",
      "phone_number_verified",
      "jansScope",
      "given_name",
      "middle_name",
      "picture",
      "name",
      "phone_number",
      "postal_code",
      "region",
      "family_name"
   ],
   "scope_to_claims_mapping":[
      {
         "openid":[
            
         ]
      },
      {
         "profile":[
            "name",
            "family_name",
            "given_name",
            "middle_name",
            "nickname",
            "preferred_username",
            "profile",
            "picture",
            "website",
            "gender",
            "birthdate",
            "zoneinfo",
            "locale",
            "updated_at"
         ]
      },
      {
         "permission":[
            "role"
         ]
      },
      {
         "^/user/.+$":[
            
         ]
      },
      {
         "http://photoz.example.com/dev/scopes/view":[
            
         ]
      },
      {
         "https://jans.io/scim/fido2.read":[
            
         ]
      },
      {
         "http://photoz.example.com/dev/scopes/all":[
            
         ]
      },
      {
         "modify":[
            
         ]
      },
      {
         "https://jans.io/scim/all-resources.search":[
            
         ]
      },
      {
         "https://jans.io/scim/groups.write":[
            
         ]
      },
      {
         "uma_protection":[
            
         ]
      },
      {
         "work_phone":[
            "work_phone"
         ]
      },
      {
         "https://jans.io/scim/users.write":[
            
         ]
      },
      {
         "https://jans.io/oauth/config/database/sql.write":[
            
         ]
      },
      {
         "phone":[
            "phone_number_verified",
            "phone_number"
         ]
      },
      {
         "address":[
            "formatted",
            "postal_code",
            "street_address",
            "locality",
            "country",
            "region"
         ]
      },
      {
         "test":[
            "member_of"
         ]
      },
      {
         "https://jans.io/oauth/config/database/sql.delete":[
            
         ]
      },
      {
         "mobile_phone":[
            "phone_mobile_number"
         ]
      },
      {
         "revoke_session":[
            
         ]
      },
      {
         "user_name":[
            "user_name"
         ]
      },
      {
         "email":[
            "email_verified",
            "email"
         ]
      },
      {
         "https://jans.io/scim/bulk":[
            
         ]
      },
      {
         "https://jans.io/oauth/config/database/sql.readonly":[
            
         ]
      },
      {
         "clientinfo":[
            "name",
            "inum",
            "jansScope",
            "jansAppType",
            "jansIdTknSignedRespAlg",
            "jansRedirectURI"
         ]
      },
      {
         "https://jans.io/scim/fido2.write":[
            
         ]
      },
      {
         "org_name":[
            "org_name"
         ]
      },
      {
         "oxd":[
            
         ]
      },
      {
         "https://jans.io/scim/users.read":[
            
         ]
      },
      {
         "https://jans.io/scim/groups.read":[
            
         ]
      },
      {
         "https://jans.io/scim/fido.read":[
            
         ]
      },
      {
         "offline_access":[
            
         ]
      },
      {
         "https://jans.io/scim/fido.write":[
            
         ]
      }
   ],
   "op_policy_uri":"http://www.jans.io/doku.php?id=jans:policy",
   "token_endpoint_auth_methods_supported":[
      "client_secret_basic",
      "client_secret_post",
      "client_secret_jwt",
      "private_key_jwt",
      "tls_client_auth",
      "self_signed_tls_client_auth",
      "none"
   ],
   "tls_client_certificate_bound_access_tokens":true,
   "response_modes_supported":[
      "fragment",
      "query",
      "form_post"
   ],
   "backchannel_logout_session_supported":true,
   "token_endpoint":"https://test.dd.jans.io/jans-auth/restv1/token",
   "backchannel_authentication_request_signing_alg_values_supported":[
      "RS256",
      "RS384",
      "RS512",
      "ES256",
      "ES384",
      "ES512",
      "PS256",
      "PS384",
      "PS512"
   ],
   "response_types_supported":[
      "token id_token",
      "token",
      "code id_token",
      "code",
      "token code",
      "token code id_token",
      "id_token"
   ],
   "backchannel_token_delivery_modes_supported":[
      "poll",
      "ping",
      "push"
   ],
   "request_uri_parameter_supported":true,
   "backchannel_user_code_parameter_supported":true,
   "grant_types_supported":[
      "authorization_code",
      "implicit",
      "urn:openid:params:grant-type:ciba",
      "client_credentials",
      "urn:ietf:params:oauth:grant-type:uma-ticket",
      "password",
      "urn:ietf:params:oauth:grant-type:device_code",
      "refresh_token"
   ],
   "ui_locales_supported":[
      "en",
      "bg",
      "de",
      "es",
      "fr",
      "it",
      "ru",
      "tr"
   ],
   "userinfo_endpoint":"https://test.dd.jans.io/jans-auth/restv1/userinfo",
   "op_tos_uri":"http://www.jans.io/doku.php?id=jans:tos",
   "auth_level_mapping":{
      "20":[
         "basic_lock"
      ],
      "10":[
         "basic"
      ]
   },
   "require_request_uri_registration":false,
   "id_token_encryption_alg_values_supported":[
      "RSA1_5",
      "RSA-OAEP",
      "A128KW",
      "A256KW"
   ],
   "frontchannel_logout_session_supported":true,
   "claims_locales_supported":[
      "en"
   ],
   "clientinfo_endpoint":"https://test.dd.jans.io/jans-auth/restv1/clientinfo",
   "request_object_signing_alg_values_supported":[
      "none",
      "HS256",
      "HS384",
      "HS512",
      "RS256",
      "RS384",
      "RS512",
      "ES256",
      "ES384",
      "ES512",
      "PS256",
      "PS384",
      "PS512"
   ],
   "request_object_encryption_alg_values_supported":[
      "RSA1_5",
      "RSA-OAEP",
      "A128KW",
      "A256KW"
   ],
   "session_revocation_endpoint":"https://test.dd.jans.io/jans-auth/restv1/revoke_session",
   "check_session_iframe":"https://test.dd.jans.io/jans-auth/opiframe.htm",
   "scopes_supported":[
      "^/user/.+$",
      "https://jans.io/scim/all-resources.search",
      "user_name",
      "clientinfo",
      "https://jans.io/scim/fido2.write",
      "work_phone",
      "https://jans.io/scim/users.write",
      "https://jans.io/scim/fido.read",
      "revoke_session",
      "https://jans.io/scim/fido.write",
      "mobile_phone",
      "https://jans.io/oauth/config/database/sql.readonly",
      "offline_access",
      "oxd",
      "org_name",
      "email",
      "https://jans.io/scim/fido2.read",
      "address",
      "test",
      "openid",
      "profile",
      "uma_protection",
      "http://photoz.example.com/dev/scopes/view",
      "permission",
      "http://photoz.example.com/dev/scopes/all",
      "https://jans.io/scim/groups.read",
      "https://jans.io/scim/bulk",
      "modify",
      "https://jans.io/scim/users.read",
      "phone",
      "https://jans.io/oauth/config/database/sql.write",
      "https://jans.io/scim/groups.write",
      "https://jans.io/oauth/config/database/sql.delete"
   ],
   "backchannel_logout_supported":true,
   "acr_values_supported":[
      "basic_lock",
      "basic"
   ],
   "request_object_encryption_enc_values_supported":[
      "A128CBC+HS256",
      "A256CBC+HS512",
      "A128GCM",
      "A256GCM"
   ],
   "device_authorization_endpoint":"https://test.dd.jans.io/jans-auth/restv1/device_authorization",
   "display_values_supported":[
      "page",
      "popup"
   ],
   "userinfo_signing_alg_values_supported":[
      "none",
      "HS256",
      "HS384",
      "HS512",
      "RS256",
      "RS384",
      "RS512",
      "ES256",
      "ES384",
      "ES512",
      "PS256",
      "PS384",
      "PS512"
   ],
   "claim_types_supported":[
      "normal"
   ],
   "userinfo_encryption_alg_values_supported":[
      "RSA1_5",
      "RSA-OAEP",
      "A128KW",
      "A256KW"
   ],
   "end_session_endpoint":"https://test.dd.jans.io/jans-auth/restv1/end_session",
   "revocation_endpoint":"https://test.dd.jans.io/jans-auth/restv1/revoke",
   "backchannel_authentication_endpoint":"https://test.dd.jans.io/jans-auth/restv1/bc-authorize",
   "token_endpoint_auth_signing_alg_values_supported":[
      "HS256",
      "HS384",
      "HS512",
      "RS256",
      "RS384",
      "RS512",
      "ES256",
      "ES384",
      "ES512",
      "PS256",
      "PS384",
      "PS512"
   ],
   "frontchannel_logout_supported":true,
   "jwks_uri":"https://test.dd.jans.io/jans-auth/restv1/jwks",
   "subject_types_supported":[
      "public",
      "pairwise"
   ],
   "id_token_signing_alg_values_supported":[
      "none",
      "HS256",
      "HS384",
      "HS512",
      "RS256",
      "RS384",
      "RS512",
      "ES256",
      "ES384",
      "ES512",
      "PS256",
      "PS384",
      "PS512"
   ],
   "registration_endpoint":"https://test.dd.jans.io/jans-auth/restv1/register",
   "id_token_token_binding_cnf_values_supported":[
      "tbh"
   ]
}
```

fido config
-----------
request:
`https://test.dd.jans.io/.well-known/fido2-configuration`

Response:
```
{
   "version":"1.1",
   "issuer":"https://test.dd.jans.io",
   "attestation":{
      "base_path":"https://test.dd.jans.io/fido2/restv1/attestation",
      "options_enpoint":"https://test.dd.jans.io/fido2/restv1/attestation/options",
      "result_enpoint":"https://test.dd.jans.io/fido2/restv1/attestation/result"
   },
   "assertion":{
      "base_path":"https://test.dd.jans.io/fido2/restv1/assertion",
      "options_enpoint":"https://test.dd.jans.io/fido2/restv1/assertion/options",
      "result_enpoint":"https://test.dd.jans.io/fido2/restv1/assertion/result"
   }
}
```
SCIM config
-----------

Request:
`https://test.dd.jans.io/.well-known/scim-configuration`

Response:
```
[
   {
      "version":"2.0",
      "authorization_supported":[
         "oauth2"
      ],
      "user_endpoint":"https://test.dd.jans.io/jans-scim/restv1/v2/Users",
      "group_endpoint":"https://test.dd.jans.io/jans-scim/restv1/v2/Groups",
      "fido_devices_endpoint":"https://test.dd.jans.io/jans-scim/restv1/v2/FidoDevices",
      "fido2_devices_endpoint":"https://test.dd.jans.io/jans-scim/restv1/v2/Fido2Devices",
      "bulk_endpoint":"https://test.dd.jans.io/jans-scim/restv1/v2/Bulk",
      "service_provider_endpoint":"https://test.dd.jans.io/jans-scim/restv1/v2/ServiceProviderConfig",
      "resource_types_endpoint":"https://test.dd.jans.io/jans-scim/restv1/v2/ResourceTypes",
      "schemas_endpoint":"https://test.dd.jans.io/jans-scim/restv1/v2/Schemas"
   }
]
```

### client registration flow

You can understand client registration flow by running below test case in `AccessTokenAsJwtHttpTest` class . It has output as given below:

```


#######################################################
TEST: accessTokenAsJwt
#######################################################
-------------------------------------------------------
REQUEST:
-------------------------------------------------------
POST /jans-auth/restv1/register HTTP/1.1
Content-Type: application/json
Accept: application/json
Host: test.dd.jans.io

{
  "access_token_as_jwt" : "true",
  "application_type" : "web",
  "scope" : "openid profile address email phone user_name",
  "redirect_uris" : [ "https://test.dd.jans.io/jans-auth-rp/home.htm" ],
  "access_token_signing_alg" : "RS512",
  "client_name" : "access token as JWT test",
  "additional_audience" : [ ],
  "response_types" : [ "code", "id_token", "token" ]
}

-------------------------------------------------------
RESPONSE:
-------------------------------------------------------
HTTP/1.1 201
Cache-Control: no-store
Connection: Keep-Alive
Content-Length: 1492
Content-Type: application/json
Date: Wed, 07 Jul 2021 08:26:48 GMT
Keep-Alive: timeout=5, max=100
Pragma: no-cache
Server: Apache/2.4.41 (Ubuntu)
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type-Options: nosniff
X-Xss-Protection: 1; mode=block

{
    "allow_spontaneous_scopes": false,
    "application_type": "web",
    "rpt_as_jwt": false,
    "registration_client_uri": "https://test.dd.jans.io/jans-auth/restv1/register?client_id=2bc0674b-48ce-4221-a19e-fa9fe7f1dc96",
    "tls_client_auth_subject_dn": "",
    "registration_access_token": "237faef9-f3c2-44b6-95fa-71951fcc5d65",
    "client_id": "2bc0674b-48ce-4221-a19e-fa9fe7f1dc96",
    "token_endpoint_auth_method": "client_secret_basic",
    "scope": "user_name email openid profile phone address",
    "run_introspection_script_before_access_token_as_jwt_creation_and_include_claims": false,
    "client_secret": "3c1fd4a6-ac97-4dde-beb4-2ceba46d0842",
    "client_id_issued_at": 1625646408,
    "backchannel_logout_uri": [],
    "backchannel_logout_session_required": false,
    "client_name": "access token as JWT test",
    "spontaneous_scopes": [],
    "id_token_signed_response_alg": "RS256",
    "access_token_as_jwt": true,
    "grant_types": [
        "authorization_code",
        "implicit",
        "refresh_token"
    ],
    "subject_type": "pairwise",
    "keep_client_authorization_after_expiration": false,
    "redirect_uris": ["https://test.dd.jans.io/jans-auth-rp/home.htm"],
    "additional_audience": [],
    "frontchannel_logout_session_required": false,
    "client_secret_expires_at": 1625732808,
    "require_auth_time": false,
    "access_token_signing_alg": "RS512",
    "response_types": [
        "token",
        "code",
        "id_token"
    ]
}

authenticateResourceOwnerAndGrantAccess: authorizationRequestUrl:https://test.dd.jans.io/jans-auth/restv1/authorize?response_type=code+id_token+token&client_id=2bc0674b-48ce-4221-a19e-fa9fe7f1dc96&scope=openid+profile+address+email+phone+user_name&redirect_uri=https%3A%2F%2Ftest.dd.jans.io%2Fjans-auth-rp%2Fhome.htm&state=214646be-513a-49b5-8344-4a8f77f42955&nonce=940ae5e7-7049-4f90-8699-4d552f5a0bba
authenticateResourceOwnerAndGrantAccess: sessionState:0ff4dccc6cc5f61d8f1c8be65572bfad2257b02677d139af63b6724042a89917.9a9c384f-736f-4364-a833-40319fac7fd9
authenticateResourceOwnerAndGrantAccess: sessionId:0af7e5fa-9ee6-4048-a87e-c9c3fc768d0e
-------------------------------------------------------
REQUEST:
-------------------------------------------------------
https://test.dd.jans.io/jans-auth/restv1/authorize?response_type=code+id_token+token&client_id=2bc0674b-48ce-4221-a19e-fa9fe7f1dc96&scope=openid+profile+address+email+phone+user_name&redirect_uri=https%3A%2F%2Ftest.dd.jans.io%2Fjans-auth-rp%2Fhome.htm&state=214646be-513a-49b5-8344-4a8f77f42955&nonce=940ae5e7-7049-4f90-8699-4d552f5a0bba

-------------------------------------------------------
RESPONSE:
-------------------------------------------------------
HTTP/1.1 302 Found
Location: https://test.dd.jans.io/jans-auth-rp/home.htm#access_token=eyJraWQiOiI1N2E3ZGQ3ZS1lMDIxLTQ1MzAtODhjNS1iZTc1NGYzNjA4Mzlfc2lnX3JzNTEyIiwidHlwIjoiSldUIiwiYWxnIjoiUlM1MTIifQ.eyJhdWQiOiIyYmMwNjc0Yi00OGNlLTQyMjEtYTE5ZS1mYTlmZTdmMWRjOTYiLCJzdWIiOiI3TXNMTEVrdDVWcWJVM3NISlF3cVE0MzVuUFJid3FBUjJwUWx2dDllZHJvIiwieDV0I1MyNTYiOiIiLCJjb2RlIjoiMmQ5NTk0NTctODA0OC00NDAxLTg4OGMtMTAzOGEzYjc1Yzg4Iiwic2NvcGUiOlsiYWRkcmVzcyIsInBob25lIiwib3BlbmlkIiwidXNlcl9uYW1lIiwicHJvZmlsZSIsImVtYWlsIl0sImlzcyI6Imh0dHBzOi8vdGVzdC5kZC5qYW5zLmlvIiwidG9rZW5fdHlwZSI6IkJlYXJlciIsImV4cCI6MTYyNTY0NjcxMiwiaWF0IjoxNjI1NjQ2NDEyLCJjbGllbnRfaWQiOiIyYmMwNjc0Yi00OGNlLTQyMjEtYTE5ZS1mYTlmZTdmMWRjOTYiLCJ1c2VybmFtZSI6IkphbnMgQXV0aCBUZXN0IFVzZXIifQ.JUHmEG6JtlBpIb8fo09Z_5mcC_SXnW1bslWyl15UBADyBwUpX-IjDtRt-mLjyJ9egVU8TQzYv2zONyvaaaU7BP4YLZ6EyQaSu37u5-MLpuIq8YscruQyd1PYnq5u4uWp5r5rUaZaMetca1bfw5fj13cyK6vr1Ls0_cObSbFaYFrJU2LweJnvYQxR_rl84DU69GMY8AxDuLTcHC9xBvm4mjts8KShRLobL1NtJY4X9tJt33kC_xMe__BvEEMqtJcczoDKI9Qs9DKDu4fha60O6S90WfLuxTMFa9RJgmsm0i9qlA_AuSVhIj5aSpFOM-6qUBiBccBaGAjiSW0SHhJO0g&code=515d2baf-5e92-41d2-b6c2-114fcb9eb8b9&scope=address+phone+openid+user_name+profile+email&id_token=eyJraWQiOiI2MGE5MzQzOC03MTA4LTQ3YjctOWY1OC0wNTIxMGJlNDlhMjdfc2lnX3JzMjU2IiwidHlwIjoiSldUIiwiYWxnIjoiUlMyNTYifQ.eyJhdF9oYXNoIjoic2lKMzNTUWJyZlhXVWFNRGNIZDI3QSIsInN1YiI6IjdNc0xMRWt0NVZxYlUzc0hKUXdxUTQzNW5QUmJ3cUFSMnBRbHZ0OWVkcm8iLCJjb2RlIjoiMzc1ZjBjMjktNTc1Ni00MzAzLTg3OTYtYTI5YWM0NzQ5Y2QwIiwiYW1yIjpbIjEwIl0sImlzcyI6Imh0dHBzOi8vdGVzdC5kZC5qYW5zLmlvIiwibm9uY2UiOiI5NDBhZTVlNy03MDQ5LTRmOTAtODY5OS00ZDU1MmY1YTBiYmEiLCJzaWQiOiI0MDA3NTBkZC1mOGUwLTRhMjUtYTZiNy0wZGI5ZmQ2N2QwN2MiLCJveE9wZW5JRENvbm5lY3RWZXJzaW9uIjoib3BlbmlkY29ubmVjdC0xLjAiLCJhdWQiOiIyYmMwNjc0Yi00OGNlLTQyMjEtYTE5ZS1mYTlmZTdmMWRjOTYiLCJhY3IiOiJiYXNpYyIsImNfaGFzaCI6InJTSUtWWDJESDIzVlAycGJUTWRDc2ciLCJzX2hhc2giOiJ1ZHc0aGRwX1FDZjZyOFE2bFM3RlJ3IiwiYXV0aF90aW1lIjoxNjI1NjQ2NDExLCJleHAiOjE2MjU2NTAwMTIsImdyYW50IjoiYXV0aG9yaXphdGlvbl9jb2RlIiwiaWF0IjoxNjI1NjQ2NDEyfQ.t9QARzZTqWvkp3QvHaD5N75sk9DAxCd9zmud2kwdg8pJ0srnI0CPKJR_69Iq5eYJsQ-bmDkfTvR4j-PdN7bZ0sAi0fwG7qqwrQpcFHRV8KV2rMpmyhajuWFbFiGY1gLz4eX1UvfaXv-YNUekEMpC4j-qWiSJyVy0tDRXFdeff5eW4M_yeqeLe-kBn1GATzYIahAUpRmdjs5blichQxAcaser2iGeDAkEnaKFYFI8UCjmZ_ICXNTS6mk5m65L3RkiDm7cDh5dbQz5b8inOwe2nPkt-BKHIOKlvpijdQlDyMBA16pjQHWNb15DK6zyZruEKSbvudiwj3PE8mNr8kW92w&session_id=0af7e5fa-9ee6-4048-a87e-c9c3fc768d0e&state=214646be-513a-49b5-8344-4a8f77f42955&token_type=Bearer&session_state=0ff4dccc6cc5f61d8f1c8be65572bfad2257b02677d139af63b6724042a89917.9a9c384f-736f-4364-a833-40319fac7fd9&expires_in=299&sid=400750dd-f8e0-4a25-a6b7-0db9fd67d07c

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 5.701 sec - in io.jans.as.client.ws.rs.AccessTokenAsJwtHttpTest

```
-----------------------------------------------------------

- list of all possible arguments to install.py is at `jans-setup` repo under `setup_app\utils\arg_parser.py`

-----------------------------


### command to setup janssen with mysql as backend:
On a blank machine, commands below will install MySQL and complete the setup.

```
wget https://raw.githubusercontent.com/JanssenProject/jans/main/jans-linux-setup/install.py > install.py
sudo python3 install.py --args="-local-rdbm=mysql"

```

it gets you the questionnair like below:

```
Do you acknowledge that use of the Janssen Server is under the Apache-2.0 license? [N|y] : y
Enter IP Address [10.160.0.4] : 
Enter hostname [temp-jans-mysql-14jul.asia-south1-a.c.conductive-coil-317212.internal] : temp.dd.jans.io
Enter your city or locality : ahm
Enter your state or province two letter code : gj
Enter two letter Country Code : in
Enter Organization Name : gluu.org
Enter email address for support at your organization : dhaval@gluu.org
Enter maximum RAM for applications in MB [13260] : 
Chose Backend Type:
  1 Local OpenDj
  2 Remote OpenDj
  3 Remote Couchbase
  4 Local MySQL
  5 Remote MySQL
  6 Cloud Spanner
Selection [1]: 4
Enter Password for Admin User [yG2v{[1c4bMj] : simplepass
Install Jans Auth Config Api? [Yes] : 
Install Scim Server? [Yes] : 
Install Fido2 Server? [Yes] : 
Install Eleven Server? [No] : 
Checking Properties

hostname                                          temp.dd.jans.io
orgName                                                  gluu.org
os                                                         ubuntu
city                                                          ahm
state                                                          gj
countryCode                                                    in
Applications max ram (MB)                                   13260
Backends                                                    mysql
Java Type                                                     jre
Install Apache 2 web server                                  True
Install Auth Server                                          True
Install Jans Auth Config Api                                 True
Install Fido2 Server                                         True
Install Scim Server                                          True
Install Eleven Server                                       False

Proceed with these values [Y|n] y
✓ jans             Calculating application memory
✓ jre              Installing Jre
✓ jetty            Installing Jetty
✓ jython           Installing Jython
✓ rdbm-server      Importing ldif files to mysql
✓ apache2          Configuring apache2
✓ jans-auth        Generating OAuth openid keys
✓ jans-config-api  Installing Jans-Config-Api
✓ jans-fido2       Installing Jans-Fido2
✓ jans-scim        Installing Jans-Scim
✓ jans-cli         Installing Jans Cli
⣻ post-setup       Starting Jans Auth


```
After installation, you can find rdbm(DB) password and other default input used by jans setup in `/opt/jans/jans-setup/setup.properties.last`

### Steps involved in DB setup during janssen installation:

For persistence types like MySQL, Janssen installer translates `.ldif` files to sql queries and executes them against db. Code flow for the same is given below. This is can only run be run on Linux as it Linux specific paths.
setup.py -> rdbmInstaller.start_installation() -> base.py.start_installation()  -> self.install() -> rdbm.py.install() -> create tables, import LDIF files and create indexes.


### Mapping of LDAP (ldif) files loaded into MySQL tables 

- ldif files in the code base are at https://github.com/JanssenProject/jans-setup/tree/master/templates and under subfolders like `jans-auth`
- base.ldif -> only one entry in table jansOrganization with `o=jans`. Not sure where rest of the data from file goes.
- attribute.ldif -> jansAttr (70 records)
- configuration.ldif -> not sure in which table is this added
- scripts.ldif -> jansCustomScr (37 records)
- jans-auth/people.ldif -> jansPerson (1 record)
- jans-auth/groups.ldif -> jansGrp (1 record)
- jans-auth/configuration.ldif, jans-config-api/config.ldif, jans-fido2/fido2.ldif, jans-scim/configuration.ldif -> jansAppConf
- templates/scopes.ldif, jans-config-api/scopes.ldif, jans-scim/scopes.ldif -> jansScope
- jans-auth/clients.ldif, jans-config-api/clients.ldif, jans-scim/clients.ldif -> jansClnt


### janssen ssl configuration:

Janssen uses apache 2 as web frontend and SSL configuration happens at the point. Not on Jetty. From the `/opt/jans/jans-setup/logs/setup.log` ... 

apache gets installed:

```
Setting up apache2 (2.4.41-4ubuntu3.3) ...
Enabling module mpm_event.
Enabling module authz_core.
Enabling module authz_host.
Enabling module authn_core.
Enabling module auth_basic.
Enabling module access_compat.
Enabling module authn_file.
Enabling module authz_user.
Enablin

```

enabling ssl and other modules
```
08:52:46 07/14/21 Running: a2enmod ssl headers proxy proxy_http proxy_ajp
08:52:46 07/14/21 Considering dependency setenvif for ssl:
Module setenvif already enabled
Considering dependency mime for ssl:
Module mime already enabled
Considering dependency socache_shmcb for ssl:
Enabling module socache_shmcb.
Enabling module ssl.
See /usr/share/doc/apache2/README.Debian.gz on how to configure SSL and create self-signed certificates.

```

generating certificates:
```
08:56:30 07/14/21 Generating Certificate for httpd
08:56:30 07/14/21 Running: /usr/bin/openssl genrsa -des3 -out /etc/certs/httpd.key.orig -passout pass:lsloW9ul0au1 2048
08:56:30 07/14/21 Running: /usr/bin/openssl rsa -in /etc/certs/httpd.key.orig -passin pass:lsloW9ul0au1 -out /etc/certs/httpd.key
08:56:30 07/14/21 Running: /usr/bin/openssl req -new -key /etc/certs/httpd.key -out /etc/certs/httpd.csr -subj /C=in/ST=gj/L=ah/O=gluu org/CN=testmysql.dd.jans.io/emailAddress=dhaval@gluu.org
08:56:30 07/14/21 Running: /usr/bin/openssl x509 -req -days 365 -in /etc/certs/httpd.csr -signkey /etc/certs/httpd.key -out /etc/certs/httpd.crt
08:56:30 07/14/21 Running: /bin/chown jetty:jetty /etc/certs/httpd.key.orig
08:56:30 07/14/21 Running: /bin/chmod 700 /etc/certs/httpd.key.orig
08:56:30 07/14/21 Running: /bin/chown jetty:jetty /etc/certs/httpd.key
08:56:30 07/14/21 Running: /bin/chmod 700 /etc/certs/httpd.key
08:56:30 07/14/21 Running: /opt/jre/bin/keytool -import -trustcacerts -alias testmysql.dd.jans.io_httpd -file /etc/certs/httpd.crt -keystore /opt/jre/jre/lib/security/cacerts -storepass changeit -noprompt
08:56:31 07/14/21 Running: /usr/bin/systemctl enable apache2
08:56:32 07/14/21 Run: /usr/bin/systemctl enable apache2 with result code: 0
08:56:32 07/14/21 Running: /usr/bin/systemctl start apache2
08:56:32 07/14/21 Run: /usr/bin/systemctl start apache2 with result code: 0
```

Other port related apache config is at [httpd_2.4.conf](https://github.com/JanssenProject/jans-setup/blob/master/templates/apache/httpd_2.4.conf) and HTTP redirection is configured in [https_jans.conf](https://github.com/JanssenProject/jans-setup/blob/master/templates/apache/https_jans.conf) file.



-----------------------
# Jans install guide with test execution and remote debugging
------------------------------------

This is a guide for setting up a development environment that enables compilation and testing of Janssen components. For a complete development environment, you need three things: 

1) Janssen server for development
   
2) Workspace which has code and tests that you can run 
   
3) Ability to remote debug 

In this guide, we will see how to setup all three above. You can setup both 1) and 2) on same machine or on different machines.

## Installing Janssen server:

When you plan to develop and contribute code to Janssen, you need a running Janssen server in order to run your tests and verify that your feature or bug fix is working as intended. You can plan to install Janssen server on local Windows machine, Linux machine or you may planning to install Janssen using Janssen cloud based deployment. 

### Hardware requirements of Janssen server

- 8 GB RAM for Janssen server installation
- CPU with at least two cores
- 40 GB harddisk space

### Platform requirements of Janssen server

Janssen auth server installs on Linux based operating system, primarily, Ubuntu. If your development environment is using a different operating system, like Windows, we have to leverage virtualization tools to install Janssen server. Follow the instructions listed in sections below as appropriate.

1) [Install Janssen on Windows OS](#installing-janssen-auth-server-on-windows-machine)
2) [Install Janssen on Ubuntu 20.4](#installing-janssen-auth-server-on-ubuntu)
3) [Install Janssen on remote server](#installing-janssen-auth-server-on-remote-server) ( like a Google Cloud Platform or AWS Linux instance )
4) On Cloud based deployment

### Installing Janssen auth server on Windows machine

Janssen runs on Linux based operating system Ubuntu. In order to run it on a Windows machine, we have to leverage virtualization technique as described in steps below.

#### Prepare your Windows machine

Steps:

    1) `TODO`
    2) `TODO`

Once you have executed above steps, your Windows machine is ready for [Janssen installation](#install-janssen).

### Installing Janssen auth server on Ubuntu

#### Prepare your Ubuntu system

Steps:

    1) `TODO`
    2) `TODO`

Once you have executed above steps, your Ubuntu machine is ready for [Janssen installation](#install-janssen).

### Installing Janssen auth server on remote server

If you have limited hardware resources on your local machine, then you may install Janssen on a remote server. For this you need to have access to a remote server, either standalone or an instance hosted on any cloud platform like GCP or AWS. Here in this guide, we will take example of installing Janssen server on an GCP instance.

#### Prepare GCP instance

Steps:

    1) `TODO`
    2) `TODO`

Once you have executed above steps, your GCP instance is ready for [Janssen installation](#install-janssen).

## Install Janssen

Janssen installation involves running two commands. During installation, setup will prompt few questions and you'll also need to accept license. During this process, among other inputs, the setup will also ask you to name your Janssen server. You can name it anyting but make note of it, as we will need that name in future. For now, we will assume that server is named *demoexample.jans.io*.

First command to run is as below. It'll download required installation script.

`wget https://raw.githubusercontent.com/JanssenProject/jans/main/jans-linux-setup/install.py`

Once you have the script, you can start installation. You can either start installation with or without test data loading along with it. Test data load will help you to run unit tests when you are writing code. You can also choose to load it later when needed.

To install with test data load:

```
sudo python3 install.py --args="-t"
```

To install without test data load:

`sudo python3 install.py`

Load test data separately from installation process: 

```
cd /opt/jans/jans-setup/
sudo python3 setup.py -t -x -n
```

After successful execution, you have a working Janssen setup. 

Now, to access Janssen end-points, please map `IP` address of your Janssen server with name of Janssen server which you provided during install process. This mapping needs to be in `/etc/hosts` file of host from where you intend to access the end-point URLs. Once this mapping is done, you can access below mentioned end-points to verify your Janssen installation:


    |Service           | Example endpoint                                                       |   
    |------------------|------------------------------------------------------------------------|
    |Auth server       | `https://demoexample.jans.io/.well-known/openid-configuration`         |
    |fido2             | `https://demoexample.jans.io/.well-known/fido2-configuration`          |
    |scim              | `https://demoexample.jans.io/.well-known/scim-configuration`           |   
    

### no prompt installation

Run commands one by one. This will uninstall install janssen with local ldap 

```
sudo python3 /opt/jans/jans-setup/install.py -uninstall -y

wget https://github.com/JanssenProject/jans/releases/download/v1.0.20.nightly/jans-1.0.20.nightly-suse15.x86_64.rpm

sudo zypper install -n ~/jans-1.0.20.nightly-suse15.x86_64.rpm

sudo python3 /opt/jans/jans-setup/setup.py -n -ip-address 10.229.38.28 -host-name jans-opensuse -city ah -state gj -country in -org-name gluu -email dhaval@gluu.org -jans-max-mem 26349 -admin-password admin -ldap-admin-password admin --listen_all_interfaces --with-casa --install-jans-keycloak-link -t
```

## Setup your workspace

#### Minimal software requirements

Most basic tools required are
- `git`  : To clone and manage the inav code repository
- `java` : Java to run maven and build. Needs Java 1.8 or above
- `mvn`  : latest maven
- Other tools like IDE etc can be of your choice

Setting up your workspace is as easy as cloning Janssen module repository from Github. You can clone the repository of the module that you intend to work on.

Here, we are going ahead with Janssen auth server module.

#### Get code

You can get code for Janssen modules from Github repository [here](https://github.com/JanssenProject)

In the directory where you want to create your workspace, you can clone the module as below:

`git clone https://github.com/JanssenProject/jans-auth-server`

#### Build

`cd jans-auth-server`

At this point, you should be able to successfully compile the module using `mvn compile`

#### Run tests

In order to be able to run tests, your code in your local workspace should be able to connect to Janssen server that you installed previously. This is done by creating a `profile` and a few more commands. That is what we will do next.

##### Create test profile 

###### What is a profile:

At the most basic level, a profile is a directory, with the same name as your server and contains files that enable your code to connect with Janssen server. In following steps, We will create profile directory where your code is and put required files under it. During it's installation, the Janssen server has already created these files for us to copy.

1) Get profile name which we will be using. Run this command where Janssen server is installated.

`cat /opt/jans/jans-setup/output/test/jans-auth/client/config-oxauth-test-data.properties | grep clientKeyStoreFile | cut -d "/" -f2 | cut -d "/" -f1`

 Output of this command is the profile name that you need to use in following steps. Generally, this name is same as name of your Janssen server.

2) Create and setup your profile
 - Setup profile for *client* module of *jans-auth-server*
   - `mkdir ./client/profiles/<profile_name>/`
   - `cp -rf /opt/jans/jans-setup/output/test/jans-auth/client/* ./client/profiles/<profile_name>/`
   - `cp ./client/profiles/default/client_keystore.jks ./client/profiles/<profile_name>/`
 - Setup profile for *server* module of *jans-auth-server*
   - `mkdir ./server/profiles/<profile_name>/`
   - `cp -rf /opt/jans/jans-setup/output/test/jans-auth/server/* ./server/profiles/<profile_name>/`
   - `cp ./server/profiles/default/client_keystore.jks ./server/profiles/<profile_name>/`

If your code and installed Janssen server is on the same machine, then at this point you should be able to [run full build](#run-full-build-with-tests) with tests. If both are on separate machines then you need to take [few additional steps](#additional-steps-for-remote-workspace) before you can run your full build with tests.

##### Additional steps for remote workspace

These steps are only needed if we need to run build and tests on a different machine then the one where you have installed Janssen server. Also its not needed if we deploy CA cert into Janssen instalation.

1) Import self signed http cert into java truststore.

Copy `/etc/certs/httpd.crt` from CE server to `<path>/httpd.crt` or run:

`openssl s_client -connect <ce-server>:443 2>&1 |sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > /tmp/httpd.crt`

`/opt/jre/bin/keytool -import -alias jans_http -keystore /opt/jre/lib/security/cacerts -file /tmp/httpd.crt`


2) Fill the right configuration `cibaEndUserNotificationConfig`. It's in `jansConfDyn` in ou=jans-auth,ou=configuration,o=jans. After restart Jans Auth server:

```
systemctl restart jans-auth
```

##### Run full build with tests:

```
mvn -fae -Dcfg=<profile_name> -Dcvss-score=9 -Dfindbugs.skip=true -Ddependency.check=false clean compile package
```

You should be able to run test cases successfully.

## Setup remote debugging

#### Changes required on Janssen server

- Open service config file

  `vim /etc/default/jans-auth`

- add line below at the end of `JAVA_OPTIONS`

  `-Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=6001`

- then restart services

  `systemctl restart jans-auth.service`
  
- (only if you are using GCP instance as jans server) add port to firewall:
  - search for firewall on dashboard search
  - edit the firewall called `default-allow-ssh`, and add port `6001`. Save settings.
  - not sure but you may want to restart your instance once for firewall settings to take effect.

#### changes required in the machine where your workspace is:

- setup port forwarding
  
  `ssh -L 6001:localhost:6001 <user>@demoexample.jans.io`
  
  this command will open an ssl connection with jans server. Keep the window open.
  
- In IntellijIdea, 
  - `shift+shift` -> search for `edit configuration` -> click on `+` -> `remote jvm debugging` -> then give below values
  - `host:` remote host IP or name as in `hosts` file, `port:` 6001, `use module:` give the module which is being debugged on server. 


#### taking mysql data dump from janssen installation
- go to /opt/jans/jans-setup/logs/setup.log
- search for `CREATE DATABASE`. this will show you the line where it has created a new database in mysql. Copy name of this db.
- now on command line, `sudo mysqldump -u root  {nameOfDB} > mysql_dump.sql`
- take this file to the pc where you want to import the data
- 


### code improvement areas

- [this code](https://github.com/JanssenProject/jans-auth-server/blob/dc30f735a9197c9ae3d882b709a24ecc0aac77d0/client/src/main/java/io/jans/as/client/RegisterClient.java#L89) has if condition that executes code based on http method of the request. Check if this can be avoided by having rest apis like what spring-boot has where methods in controller are called based on http request method and `if` check is not required.
- 


### misc notes :

- while trying to setup local workspace, i tried running jans-auth-server.war on Jetty 10.0 but it failed to start due to sax exception in parcing jetty-env.xml. It worked fine when I tried on jetty 9 (jetty-distribution-9.4.31.v20200723.tar.gz) as downloaded from one of the installed janssen server instance from location (/opt/dist/app/jetty-distribution-9.4.31.v20200723.tar.gz).
- when you are running tests via maven on command line, and there are failure, and you want to see which tests are failing then 
  - push output in a file `mvn -Dcfg=test.local.jans.io -fae -Dcvss-score=9 -Dfindbugs.skip=true -Ddependency.check=false clean compile test &> ~/temp/log_server_WithAddingServerCertInJreCAcerts.4.log`
  - then grep `grep -nR ' FAILURE' ~/temp/log_server_WithAddingServerCertInJreCAcerts.4.log`
  - first line is summary and last line can be ignored.
- janssen default labels are [here](https://github.com/organizations/JanssenProject/settings/repository-defaults)
- In `codeql` and `code quality check` janssen github actions, there is a basic difference. While both try to build the project, `CodeQL` builds all dependency projects first and then lastly build current project (see jans-fido). Where `code quality check` directly builds current project. So, `codeql` project uses freshly built dependency artifacts, while `code quality check` downloads everything form maven repo. So if there is a code change that is in master but not reached maven yet, then build might get impact of same.
- when you install jans using install.py on lxc, then you can access endpoints from host machine browser using
  ```
  https://<ip-of-lxc-instance>/.well-known/openid-configuration
  ```
  no need to open any port like 443 or 8443.




### Imp Janssen commands
- `systemctl list-units --type=service --state=running` find all running services [reference](https://www.codegrepper.com/code-examples/shell/how+to+check+if+port+80+is+binded+to+apache+ubuntu)
- `systemctl status jans-auth.service`: To know status of Janssen auth server service
- `systemctl restart jans-auth`: Restart Janssen auth service
- `systemctl list-units --all "jans*"`: To know status of all Janssen services
- `systemctl list-units --all "*opendj*"`: To check if opendj ldap service is running or not
- `mvn -Dcfg=test.jans.gluu.org -Dmaven.test.skip=false -Ddevelopment-build=false -Dcvss-score=9 -Dfindbugs.skip=true -Ddependency.check=false clean compile install javadoc:javadoc findbugs:findbugs site`: maven build command for jans-auth-server
- file that holds JVM parameters and other environment variable: `vim /etc/default/jans-auth`. Similarly, there are files for fido2, SCIM etc in same folder.
- `sudo journalctl -u [service_name]` will show you logs of systemctl. Not very useful but thats where it all starts. e.g `sudo journalctl -u jans-auth.service`
- Janssen config files are stored under `/etc/jans/conf/`. For example, `jans-ldap.properties`
- Janssen code: generating javadoc for janssen modules : `dhaval@thinkpad:~/IdeaProjects/Janssen/jans-auth-server$ mvn javadoc:javadoc`. After this, you can find javadoc in target folder. eg `file:///home/dhaval/IdeaProjects/Janssen/jans-auth-server/model/target/site/apidocs/io/jans/as/model/configuration/Configuration.html`
- List of endpoints for janssen after installation: `https://github.com/JanssenProject/jans-setup/blob/master/templates/jans-auth/jans-auth-config.json`
- for any jans setup, file that contains all the installation options as well as parameters with which jans gets installed are in `/opt/jans/jans-setup/setup.properties.last`. This file also has password for default jans user, which is `admin`
- know Janssen version: `/opt/jans/bin/show_version.py`


### Similar to janssen/Gluu:

1) [Curity](https://curity.io/): they also have a community edition like Gluu.
2) [Authlete](https://www.authlete.com/): They don't have a community edition but they have a strong team.
3) [ory](https://github.com/ory/kratos)
4) [keycloak](https://github.com/keycloak/keycloak)


### Run janssen test suite using intellij IDE:

- go to `run/configuration'
- click on `+` on top left corner to add new configuration
- select `testng`
- and then select `suite`, give path to `testng.xml`. Remove existing `-ea` vm param and give `VM options` as required. Note: At times you'l see that `vm options`  are not being effective. To fix this, put same params in `test runner params`.
- save and run

![image](/images/testng-intellij.png)

This should bring up `run` tool window at the bottom of IDE and on left of that window you should be able to see status of each test as they get executed. Remember:
- green tick is pass
- grey `no go` symbole is `ignored` test
- amber `cross` is failed test
- red `cross` is error while executing test

![image](/images/testng-intellij-2.png)


### Code of your project build on Jenkins:
For a particular build, if you want to check code on which the build happend, 
```
go to build -> workspace
```
You can see the exact code on which the build happend and artifacts that build generated just like your local workspace. For example, you can download test reports etc from here.


### how to change log level on an installed janssen server

Changing the log level involves changing JSON config stored in Persistence. If you are using mysql as persistence, you have to change JSON value stored in 

```
SELECT jansConfDyn FROM jansdb.jansAppConf where doc_id = "jans-auth";
```

In above JSON value, you have to change value for entry `loggingLevel` to `TRACE`.

after this restart jans auth service using

```
sudo systemctl restart jans-auth.service
```

Once you do this, you'll see that logs at below location has started logging the debug and trace logs:

```
/opt/jans/jetty/jans-auth/logs/jans-auth.log
/opt/jans/jetty/jans-auth/logs/jans-auth_persistence.log
```

If you have changed the log level to trace, you can see incoming requests and processing of the same in jans-auth.log like below:

```
2022-06-11 00:24:18,789 TRACE [qtp902478634-21] 020b807c-b8f7-4d53-9394-40c09acd7136 [io.jans.as.server.auth.AuthenticationFilter] (AuthenticationFilter.java:158) - Get request to: 'https://janssen.op.io/jans-auth/restv1/userinfo'
```

Also, gluu documentation has this way of changing log level without changing persistence. But I couldn't do it for Jans :

https://gluu.org/docs/gluu-server/4.3/operation/logs/#log-levels

See the section `Changing Log Levels using log4j2.xml`
## Usecases

### References:
- good short video on oauth2 flow. Can be used for Janssen tutorial as well. https://www.youtube.com/watch?v=CPbvxxslDTU

### Good online tool for curl
https://reqbin.com/curl

### jans instance for automated daily deployment
https://jans-ui.jans.io/admin


### debugging custom(interception) scripts

Logs are at: /opt/jans/jetty/jans-auth/jans-auth_script.log

### error logs for jans-cli
/opt/jans/jans-cli/error.log


### Create new user using scim cli

- Copy file content from [here](https://raw.githubusercontent.com/maduvena/jans-docs/main/create-user.json) and store it in a file, say `~/create-user.json`.
- Then run command below to create the user

```
/opt/jans/jans-cli/scim-cli.py --operation-id create-user --data /tmp/create-user.json
```

## useful curl commands

### accessing userinfo endpoint and getting data about a user

- Get access token using client `jans config api`, its secret and scope `https://jans.io/scim/users.read`. Get details about
client from TUI

```
curl -k -u "1802.c0547ae9-d667-4b5d-8f4e-29556d5cc138:vajPeuiywXHf" https:/jans-dynamic-ldap/jans-auth/restv1/token -d  "grant_type=client_credentials&scope=https://jans.io/scim/users.read"

curl -k https://jans-dynamic-ldap/jans-auth/restv1/userinfo -H "Authorization: Bearer 5b37e8fa-e4ed-435c-9ab4-3f62261c6815"
```
## TUI

- TUI uses config-api always. Doesn't connect directly with auth-server or any other backend api.


## useful config-cli commands


Enable debug by adding 

```shell
debug = true
log_dir = /opt/jans
```

as first lines into

```shell
vim ~/.config/jans-cli.ini
```

restart cli session if already open. Debug logs are available at

```shell
vim /opt/jans/cli_debug.log
```

Get help. This lists all the possible commandline args for cli. It also lists all the possible
operations as arguments for `--info` 

```shell
/opt/jans/jans-cli/config-cli.py --help
```

To get information about an operation 

```shell
/opt/jans/jans-cli/config-cli.py --info DefaultAuthenticationMethod
or
/opt/jans/jans-cli/config-cli.py --info OauthOpenidConnectClients
```

Each operation is made up of multiple `operation-id`. An operation-id may have a schema associated.
Find that from output of above command. Find information about schema using:

```shell
/opt/jans/jans-cli/config-cli.py --schema AuthenticationMethod
or
/opt/jans/jans-cli/config-cli.py --schema Client
```

## jans-tent

Once you have setup and run the jans-tent using [these]() instructions, to run in next time, you just have to follow below steps:

```
cd IdeaProjects/Janssen/jans-for-tent/jans/demos/jans-tent/
source venv/bin/activate
python main.py
```

### Troubleshooting jans tent:

- Error: where server says the client is not authorized to make this request.

 Here you should check if the client exists or the server or not. Many times when I tried to start testing on a new day, the client with `jans tent client` from previous day did not exist on server. I don't know why. 
 Solution: run the `python register_new_client.py` command and then start the main program again by runnnig `python main.py`

- Error: mismatching_state: CSRF Warning! State not equal in request and response.

This is when there is a mismatch between name of the host mentioned in the redirect URI for the client used by Jans-tent, and the host name mentioned in the url used in browser to initiate the flow. See [this issue](https://github.com/JanssenProject/jans/issues/4617)

### gluu.org

[https://www.gl uu.org](https://glu u.org/)https://g luu.org/ is hosted on www.glu u.org and can be connected using `ssh -p 22222 -i ~/.ssh/id_rsa root@w ww.g luu.o rg` while on VPN.

swagger UI is hosted at `/opt/wordpress/swagger-ui/`

apache is under `/etc/apache2`

in order to configure using [config parameters](https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration/), you have to edit `vim /opt/wordpress/swagger-ui/index.html` and add configuration parameters like below:
```
    <script src="./swagger-ui-bundle.js"> </script>
    <script src="./swagger-ui-standalone-preset.js"> </script>
    <script>
    window.onload = function() {

      // Build a system
      const ui = SwaggerUIBundle({
        url: "https://raw.githubusercontent.com/GluuFederation/oxd/version_4.0.0/oxd-server/src/main/resources/swagger.yaml#/developers/setup-client",
        dom_id: '#swagger-ui',
        deepLinking: true,
        defaultModelRendering: "model",    
        presets: [
          SwaggerUIBundle.presets.apis,
          SwaggerUIStandalonePreset
```

If you are running newer version of swagger UI, you have to edit `vim /var/www/html/swagger-initializer.js` to add config variables.

after adding config variables, just save the file and refresh the webpage on browser. Effect should be visible.

## jans-lock

Understanding the OPA: 

This is based on https://play.openpolicyagent.org/

OPA is like this equation: 

```
input+(policy+data(user-role-mapping, role-action-subject-mapping)) = Output(allow/disallow)
```

OPA has 4 parts:

- input (this is transactional, current incoming data which talks about the action being performed. By whom, on what, what action)
- data (this is mapping of role-user, and also which role can do what action on which data)
- policy (this is the logic or rules which derives whether to give permission or not. Policy basically takes input, looks at data and decides whether the input is eligible to take the requested action or not)
- output: usually one of the output is allow/deny. There can be other outcomes also after policy execution.

Important notes:

- Here, the data basically has all the knowledge about what should be allowed and what should be not. All that policy does is to put this knowledge in the context of the input and give output.
- Data is the admin data and user data. Like user-role mapping, role-action-subject mappings etc. Hence data can be a collection of multiple sets of data. 


## installing flex

I was able to install flex using [these instructions](https://docs.gluu.org/v5.0.0-20/install/vm-install/suse/). Below are few points to take care of. 

Once after the installation, when I tried accessing admin UI, it showed below. According to a chat from Arnab, it could be because of two reasons. One if the license is obtained from dev, or the VPN is off. 
![image](https://github.com/ossdhaval/mysite/assets/343411/71f75e83-18dd-4589-af93-488c34477b6e)

So I turned on the VPN as my license was from PROD already. But after that when I click on `start 30 day trial`, it gives a screen with message as `bad gateway`. But when I still click on `start 30 day trial`, this message goes away and admin login page is shown and admin-ui is accessible. 


## Create easy cloud VM

Easycloud github action is setup to provide you a blank infrastructure (VM or Kub) with nothing installed (no jans, no flex, just OS).

- go to this action in https://github.com/GluuFederation/easycloud/actions/workflows/create_ephemerals_envs.yml
- click on `run workflow button`. It'll give you a popup form to fill.
- To create a VM on AWS with 2 core and 8 GB, Ubuntu22.04 for 12 hours use the following inputs
 - ![image](https://github.com/ossdhaval/mysite/assets/343411/633e8bb4-406a-4444-a5fd-b25efd090fdf)
 - ![image](https://github.com/ossdhaval/mysite/assets/343411/e9ef6875-ba48-4045-9e9b-dacffa2349db)
- click on run workflow. You should see a workflow created in the list and also a PR getting created with title like `ci: ossdhaval`. This PR has IP of the system and FQDN of the system. You'll need both of these when installing jans or flex later.
- This PR stays open till your environment is alive, and gets closed based on the date and time mentioned in its description. If you want to kill an environment quickly then just update the PR description and set the date to yesterdays.
- Also, you'll get a message on `#bot_reporter` channel with a pem file in it.
- download that pem file.
- change the permissions of the pem file : `chmod 600 private.pem`
- To access the environment via ssh, run this command `ssh -i <path-to-pem> ubuntu@<IP>`. For ubuntu the user is `ubuntu`, (else try `ec2-user`) as well. Check PR description for more info if it dosn't work.
- Now you can install jans as in a local lxc vm. Just remember to give the domain name as FQDN during the setup.


## How to get to various UI screens of Janssen Server?

### Authorization (consent gathering) screen

- Using Jans Tarp, create a new client with all the default values. This will create an untrusted client
- Initiate an authorization code flow.
- This should first give you a authentication screen and then show the authorization screen. Even if there are no scopes attached to request.

### account selection screen

- Using Jans Tarp, create a new client with all the default values. This will create an untrusted client
- Initiate an authorization code flow.
- This should first give you a authentication screen where you login as a user, let's say `admin`. Tarp will show the user details page with a logout button. Don't logout and leave the page open.
- then you open another tab in the same browser and open tarp.
- tarp will show the client details where under `additional params` text box, add `{"prompt":"select_account"}`
- Initiate an authorization code flow.
- This will show you a page where you can select the account (existing admin login, or add another one) like below
  ![image](https://github.com/ossdhaval/mysite/assets/343411/012a875d-65a5-4daf-b2f6-23ec9ac12843)
- upon selecting `login as another user`, you'll be redirected to the authentication screen again where you can login
