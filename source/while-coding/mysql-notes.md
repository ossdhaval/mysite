- login to mysql 
  ```
  sudo mysql -u <username> -p <schema-name>
  ```
  it'll ask for password for `username`

- Get list of all users.

  ```
  select user from mysql.user;
  ```

Get list of all available schemas (DBs)

  ```
  SHOW DATABASES;
  ```

get list of all all available tables in current schema.

  ```
  show tables;
  ```

## Troubleshooting

when trying to connect with MySQL instance on local host from mysql workbench, I faced error as below:

```
An AppArmor policy prevents this sender from sending this message to this

```

Solution :
`sudo snap connect mysql-workbench-community:password-manager-service :password-manager-service`
reference : [here](https://askubuntu.com/questions/1242026/cannot-connect-mysql-workbench-to-mysql-server)
