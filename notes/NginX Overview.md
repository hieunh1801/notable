---
attachments: [Clipboard_2020-07-21-10-06-26.png]
title: NginX Overview
created: '2020-07-21T03:04:44.998Z'
modified: '2020-07-21T03:23:24.464Z'
---

# NginX Overview
- Web server
- __Reverse proxy__: reverse proxy (hay là proxy server) trung gian nhận yêu cầu từ Internet và chuyển tới các máy chủ (servers) trong mạng cục bộ (LAN). 
![](@attachment/Clipboard_2020-07-21-10-06-26.png)

## Install && Command
```bash
# update package
sudo apt-get update

# install nginx
sudo apt-get install nginx

# check nginx installed
sudo nginx -v
```

## Cấu hình NGINX
- Webserver sẽ được cài đặt tại thư mục  /etc/nginx/. Tất cả các cấu hình sẽ được cấu hình tại đây.
- 2 cái quan trọng nhất:
  - File __nginx.config__: chứa cấu hình nginx
  - Folder __sites-available__
