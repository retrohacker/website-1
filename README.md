# Functions Conf Website

### Local Development

To run locally, start by installing `Docker` & `Docker Compose`, then follow these steps to generate an SSL certificate for local usage:

#### Create CA key and cert

```bash
cd ssl
openssl genrsa -out root.key 2048
openssl req -x509 -new -nodes -days 3650 -config openssl.cnf -key root.key -out root.pem
openssl req -new -nodes -newkey rsa:2048 -config openssl.cnf -keyout localhost.key -out localhost.csr
openssl x509 -req -in localhost.csr -CA root.pem -CAkey root.key -CAcreateserial -out localhost.crt -days 3650 -sha256 -extfile v3.ext
```

#### Add cert to the browser

```
Chrome -> Setting -> (Advanced) Manage Certificates -> Import -> 'root.pem'
```