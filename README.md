# nginx-self-signed

Generate a self-signed certificate:
```bash
mkdir -p certs

openssl req -x509 -nodes -days 3650 \
  -newkey rsa:2048 \
  -keyout certs/server.key \
  -out certs/server.crt \
  -subj "/CN=nginx"
```

Start containers:
```bash
docker-compose up -d
```

Enter netshoot container:
```bash
docker exec -it netshoot bash
```

Then test HTTPS:
```bash
curl -v https://nginx
```

To trust the cert inside netshoot:
```bash
curl --cacert /root/certs/server.crt https://nginx
```

To view the certificate details of nginx:
```bash
openssl s_client -connect nginx:443 -showcerts < /dev/null
```
