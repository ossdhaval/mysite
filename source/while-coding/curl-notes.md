# curl notes

## Resources: 
- Very good site to learn and try out : https://reqbin.com/curl
- curl official tutorial: https://curl.se/docs/manual.html
- curl official book: https://everything.curl.dev/


##### detailed info about request response

```
curl -v http://google.com

```

more details

```
curl --trace-ascii ./temp/debugdump.txt https://www.google.com

```

##### Send GET

```
curl https://www.google.com
```

##### send POST

```
curl -X POST https://www.google.com
```

##### custom port

```
curl https://localhost:4444
```

##### send request parameters

```
curl --data-urlencode "name=I am Daniel" http://www.example.com
```

##### curl with ignore self-signed certificates
use `-k`

```
curl -X POST -k https://127.0.0.1:443/.well-known/openid-configuration
```

##### send json data with post

```
curl -X POST https://reqbin.com/echo/post/json
   -H 'Content-Type: application/json'
   -d '{"login":"my_login","password":"my_password"}'
```

##### POST JSON File

```
curl -X POST https://reqbin.com/echo/post/json -d @filename
```

##### userid-password for basic authentication

This can be done using `-u`. For example 

```
curl -k -u "FF81-2D39:FF81-2D39-jans-dynamic-ldap" https://jans-dynamic-ldap/jans-auth/restv1/token -d  "grant_type=client_credentials&scope=token"
```

In the request this will be converted to header like below. User name and password string gets converted in base64 encoded string as below.

```
Authorization: Basic RkY4MS0yRDM5OkZGODEtMkQzOS1qYW5zLWR5bmFtaWMtbGRhcA==
```
