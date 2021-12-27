- login to mysql 
  ```
  sudo mysql -u <username> -p <schema-name>
  ```
  it'll ask for password for `username`

- Get list of all users.

  ```
  select user from mysql.user;
  ```

- drop a user

  ```
  sudo mydql (to log in as super user)
  drop user gluu@localhost;
  ```

- Get list of all available schemas (DBs)

  ```
  SHOW DATABASES;
  ```

- get list of all all available tables in current schema.

  ```
  show tables;
  ```

- get information about table:

```
describe <tablename>
```

- Inserting text with double quotes and new lines.

To do this, you have to surround value by single quotes.

```
update jsontest set json2 = '{"keys" : [ {
    "descr" : "Signature Key: RSA RSASSA-PKCS1-v1_5 using SHA-256",
    "kty" : "RSA",
  }]}'
    where json1 = "json";
```

- import data dump sql file
```
sudo mysql -u root -p jansdb < /root/jansdb_withtestdata_dump_15_nov_2021.sql
```

- create a data dump of a schema

```
mysqldump -u root -p gluudb > ~/gluudb-dump.sql
```

## Troubleshooting

when trying to connect with MySQL instance on local host from mysql workbench, I faced error as below:

```
An AppArmor policy prevents this sender from sending this message to this

```

Solution :
`sudo snap connect mysql-workbench-community:password-manager-service :password-manager-service`
reference : [here](https://askubuntu.com/questions/1242026/cannot-connect-mysql-workbench-to-mysql-server)
