---
title: Generate OPEN SSL for https
created: '2020-06-26T03:40:53.807Z'
modified: '2020-06-26T03:48:43.501Z'
---

# Generate OPEN SSL for https
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout server.key -out server.cert
```
