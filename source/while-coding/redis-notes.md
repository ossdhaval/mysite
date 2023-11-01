# Redis Notes

## Install redis

- get a ubuntu VM or create a lxc
- run commands given below:
  ```
  sudo apt install lsb-release curl gpg
  curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
  echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list
  sudo apt-get update
  sudo apt-get install redis
  ```
- check if redis is installed fine:
  ```
  systemctl status redis-server.service
  ```
## Configure redis

- Redis config file is at `/etc/redis/redis.conf`. Note that restart redis server after you make any change in this file, using `systemctl restart redis-server.service`
- Redis log file is at `/var/log/redis/redis-server.log`

## Setup redis cluster

- to create redis cluster, [this](https://redis.io/docs/management/scaling/#create-a-redis-cluster) is a good link.
- essentially, you first need to have few redis instances running and then with one command you make them into a cluster
- There are few important configuration items which I encountered during my troubleshooting. It is listed below along with corresponding error
 that it solved.
- Another thing, redis cluster is ideal if you have heavy load and you want scalability. If you just want a central cache with high-availability
 then there is another redis high-available configuration which is separate from cluster. 

---------------------------------------------------------------------------------------------  
redis-cli INFO Replication

# Replication
role:master
connected_slaves:0
master_failover_state:no-failover
master_replid:61f9842bb857d92ab7d55255be8f0c713627c073
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0


	

ERR This instance has cluster support disabled


----------- fix -------------------------------

 update the /etc/redis/redis.conf

 cluster-enabled yes
 cluster-config-file nodes-6379.conf
 cluster-node-timeout 15000

and then restart redis server

systemctl stop redis-server.service
systemctl start redis-server.service

-----------------------


you see this in the server logs/var/log/redis/redis-server.log :

1684:C 31 Oct 2023 13:49:57.039 * Configuration loaded
1684:M 31 Oct 2023 13:49:57.039 * monotonic clock: POSIX clock_gettime
1684:M 31 Oct 2023 13:49:57.040 * Running mode=cluster, port=6379.
1684:M 31 Oct 2023 13:49:57.040 * No cluster configuration found, I'm fd7c05b19dabbb030f0b0f1eb5c9817c20e1dcf2
1684:M 31 Oct 2023 13:49:57.063 * Server initialized


---------------------------------------




redis-cli --cluster create 10.229.38.197:6379 10.229.38.96:6379 10.229.38.183:6379 10.229.38.97:6379 10.229.38.122:6379 10.229.38.45:6379 --cluster-replicas 1



--------------
getting error


Could not connect to Redis at 10.229.38.197:6379: Connection refused

------------ fix

in redis.conf update bind address

bind 10.229.38.197 -::1

after this redis started listening on 10.229.38.197:6379 and the connection refused error went away.

But started getting error as below

-----------------

[ERR] Node 10.229.38.197:6379 DENIED Redis is running in protected mode because protected mode is enabled and no password is set for the default user. In this mode connections are only accepted from the loopback interface. If you want to connect from external computers to Redis you may adopt one of the following solutions: 1) Just disable protected mode sending the command 'CONFIG SET protected-mode no' from the loopback interface by connecting to Redis from the same host the server is running, however MAKE SURE Redis is not publicly accessible from internet if you do so. Use CONFIG REWRITE to make this change permanent. 2) Alternatively you can just disable the protected mode by editing the Redis configuration file, and setting the protected mode option to 'no', and then restarting the server. 3) If you started the server manually just for testing, restart it with the '--protected-mode no' option. 4) Set up an authentication password for the default user. NOTE: You only need to do one of the above things in order for the server to start accepting connections from the outside.


-------------fix -------------
uncommented below line
requirepass foobared

and kept below line as it is
protected-mode




--------------------------

getting 

[ERR] Node 10.229.38.197:6379 NOAUTH Authentication required.

-------

and changed the cluster create command to (added -a)

redis-cli -a 'foobared' --cluster create 10.229.38.197:6379 10.229.38.96:6379 10.229.38.183:6379 10.229.38.97:6379 10.229.38.122:6379 10.229.38.45:6379 --cluster-replicas 1

this resolved the above error.

---------------------




AUTH <password>

AUTH default <password>

