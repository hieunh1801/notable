---
title: Nginx Scenario
created: '2020-07-21T03:35:43.579Z'
modified: '2020-07-21T03:44:59.492Z'
---

# Nginx Scenario

<details open>
<summary>Revert Proxy</summary>

- __Mô tả__: đóng vai trò trung gian khi giao tiếp với bên ngoài. VD:
  - Ta có một server chạy bằng nodejs chạy trên cổng 8001
  - Ta muốn public nó ra ngoài sử dụng nginx server sử dụng cổng 8000.

- __Implement__:
  - Step 1: cấu hình nginx server. Mở file __/etc/nginx/nginx.conf__
```txt
http {
  server {
		listen 8000; # lắng nghe cổng 8000 từ ngoài vào
		listen [::]:8000; 
    # location /: tính từ đường dẫn là 172.22.22.22:8000/
		location / {
			proxy_pass http://localhost:9001/; # trỏ tương ứng tới cổng 9001 đang chạy
		}
	}
}
	
```

</details>


<details close>
<summary>R</summary>
Details...
</details>
