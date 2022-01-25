# Steps for installing jans using vmware and rancher
- after installing VM using VMWare (4 core, 4.2gb mem, 80gb hdd, ubuntu 20.0.4)
- note down ip of your vm (`ip a` -> ip against `inet`. e.g: 192.168.223.128)
- sudo apt install curl
- curl -fsSL https://get.docker.com -o get-docker.sh
- sudo sh get-docker.sh
- sudo docker run -d --restart=unless-stopped -p 80:80 -p 443:443 --privileged rancher/rancher:latest
