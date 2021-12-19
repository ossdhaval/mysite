# curl notes

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
