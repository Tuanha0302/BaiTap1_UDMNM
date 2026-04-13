# E. Triển khai (level test) ứng dụng

- Chuyển vào trong thư mục ~/myapp
- Gõ lệnh để docker compose chạy: sẽ run tất cả các service khai báo trong file docker-compose.yml
- Lợi ích: Chỉ cần docker-compose up -d là toàn bộ hệ thống (Web + Node-RED + Tunnel) tự chạy
```
version: "3.8"

services:
  nodered:
    image: nodered/node-red
    container_name: nodered
    ports:
      - "1880:1880"
    volumes:
      - ./nodered:/data
    restart: always

  nginx:
    image: nginx:latest
    container_name: nginx
    ports:
      - "80:80"
    volumes:
      - ./myweb:/myweb
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - myapi
    restart: always

  myapi:
    build: ./myapi
    container_name: myapi
    ports:
      - "9630:9630"
    restart: always

  cloudflared:
    image: cloudflare/cloudflared:latest
    container_name: cloudflared
    command: tunnel --no-autoupdate run --token ${CF_TOKEN}
    volumes:
      - ~/.cloudflared:/etc/cloudflared
    depends_on:
      - nginx
    restart: always
```

Kiểm tra các container đang chạy trong docker, nếu có cái nào bị restart cần tìm lỗi rồi edit lại docker-compose.yml

<img width="711" height="381" alt="loi cf" src="https://github.com/user-attachments/assets/ca7952b3-d70d-40d4-8009-eb76be61e0d3" />

Kiểm tra kiểm thử các service đang chạy độc lập thông qua ip và port của nó: ví dụ mở trình duyệt ip_ubuntu:1880 để check nodered đã chạy chưa

<img width="960" height="424" alt="nodered ok" src="https://github.com/user-attachments/assets/1043f871-e8fc-47ad-ab9f-b0b28afd5958" />
