# nginx-self-signed

Generate a self-signed certificate:
```bash
mkdir certs

openssl req -x509 -nodes -days 365 \
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
