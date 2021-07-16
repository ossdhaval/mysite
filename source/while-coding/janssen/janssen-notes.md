Note : many times docs mention that run this command from 'Inside the Gluu Server chroot', or 'run it from gluu container' etc. All this means one thing that you first login to the gluu container using

/sbin/gluu-serverd login
and then run commands.


==================================

 Janssen local install installation instructions :

===================================

https://github.com/JanssenProject/jans-setup

cd ~

dhaval@dhaval-Lenovo-U41-70:~$ curl https://raw.githubusercontent.com/JanssenProject/jans-setup/master/install.py > install.py

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



Uninstall

----------



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

==================================

 Janssen local install using lxd instructions :

===================================

snap install lxd

snap refresh

lxd init # Default settings looks good. I only specified 'dir' (question 4) storage method to access container filesystem /var/snap/lxd/common/lxd/storage-pools/default/containers/ubuntu20/rootfs/

lxc launch images:ubuntu/20.04/amd64 ubuntu20

lxc config device add ubuntu20 myport443 proxy listen=tcp:0.0.0.0:443 connect=tcp:127.0.0.1:443

lxc config device add ubuntu20 myport1636 proxy listen=tcp:0.0.0.0:1636 connect=tcp:127.0.0.1:1636

lxc config set ubuntu20 limits.memory 4GB

lxc exec ubuntu20 -- sudo --user root --login

apt install curl

curl https://raw.githubusercontent.com/JanssenProject/jans-setup/master/install.py > install.py

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





=============
enable linux GUI on GCP vm
================
I tried with these steps
https://medium.com/@jhsperc/gce-ubuntu-desktop-18-04-anydesk-42a21cf8821c#:~:text=Make%20sure%20you%20setup%20a,you%20are%20to%20your%20desktop.
but failed at the end when I was trying to connect via anydesk with error
"remote display server is not supported ( eg wayland )"


=============================
general notes :
main component in Janssen and Gluu is jans-auth-server. Same component is 
called oxauth in Gluu.

======================

LDAP/opendj/dsconfig commands :

to see all the existing indexes on backend 'userRoot':

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




### code improvement areas

- [this code](https://github.com/JanssenProject/jans-auth-server/blob/dc30f735a9197c9ae3d882b709a24ecc0aac77d0/client/src/main/java/io/jans/as/client/RegisterClient.java#L89) has if condition that executes code based on http method of the request. Check if this can be avoided by having rest apis like what spring-boot has where methods in controller are called based on http request method and `if` check is not required.
- 


### Imp Janssen commands

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

### Similar to janssen/Gluu:

1) [Curity](https://curity.io/): they also have a community edition like Gluu.
2) [Authlete](https://www.authlete.com/): They don't have a community edition but they have a strong team.