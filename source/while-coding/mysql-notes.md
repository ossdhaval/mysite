Get list of all users.

`select user from mysql.user;`

Get list of all available schemas (DBs)

`SHOW DATABASES;`


## Troubleshooting

when trying to connect with MySQL instance on local host from mysql workbench, I faced error as below:

```
An AppArmor policy prevents this sender from sending this message to this

```

Solution :
`sudo snap connect mysql-workbench-community:password-manager-service :password-manager-service`
reference : [here](https://askubuntu.com/questions/1242026/cannot-connect-mysql-workbench-to-mysql-server)
