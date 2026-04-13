# C. Cấu hình docker compose:
- Tạo thư mục: ~/myapp
- Chuyển vào trong thư mục ~/myapp
- Tạo thư mục: ./myweb
- Tạo file ./myweb/index.html (với nội dung là thông tin cá nhân của em)
  
<img width="658" height="251" alt="lenh" src="https://github.com/user-attachments/assets/9d80edd0-e4cd-4e90-9c87-641e866569f1" />

Tạo file docker-compose.yml để nó sẽ có các dịch vụ sau:
- Khai báo sử dụng nodered/node-red, cổng 1880, dữ liệu nằm tại thư mục ./nodered
- Khai báo sử dụng nginx, cổng 80, cấu hình trong file ./nginx/nginx.conf
- Mount thư mục ./myweb thành thư mục /myweb trong nginx
- Mount file ./nginx/nginx.conf vào file /etc/nginx/nginx.conf trong nginx

<img width="662" height="381" alt="docker-compose yml" src="https://github.com/user-attachments/assets/751137b7-daba-48a2-b389-9ba9d2d64e9d" />

Edit file ./nginx/nginx.conf để:
- Cấu hình web server cổng 80
- server_name là sub-domain (sub-domain tuỳ ý của em)
- location / trỏ tới root là thư mục /myweb
- location /api dùng proxy_pass trỏ tới 1 (hoặc nhiều) node http_in của nodered

<img width="657" height="381" alt="nginx conf" src="https://github.com/user-attachments/assets/f100095b-7d5e-4622-b8a5-8b4ff0564bac" />

Edit file ./nodered/settings.js để nodered bắt buộc đăng nhập. 

Chạy docker-compose lần đầu để Node-RED tự sinh file cấu hình trong thư mục ./nodered, sau đó mới tiến hành sửa settings.js và restart lại container
Tiếp theo sinh hash-pw bằng lệnh `docker exec -it nodered node-red admin hash-pw`.

Nó sẽ hỏi password, nhập password bạn muốn (lưu ý: nó không hiện chữ khi nhập)

<img width="662" height="38" alt="hash pw" src="https://github.com/user-attachments/assets/4d4d9cdd-b093-4eb7-aa15-92e9d512c207" />

Sau đó copy paste hash-pw đó vào setting.js, nên chú thích bên cạnh để không quên

<img width="661" height="308" alt="en pass nodered" src="https://github.com/user-attachments/assets/f0966acd-4cc8-4670-8fd4-d442f931549e" />

**Sau khi xong hết phần C ta được kết quả**
<img width="960" height="402" alt="nginx ok" src="https://github.com/user-attachments/assets/d83c7cdf-e95f-4b0b-ab65-b7484c3a3de3" />

<img width="960" height="410" alt="nodered pass ok" src="https://github.com/user-attachments/assets/590d0719-ba2e-4277-98ad-118998340230" />

