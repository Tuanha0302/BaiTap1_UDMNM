# C. Cấu hình docker compose:
- Tạo thư mục: ~/myapp
- Chuyển vào trong thư mục ~/myapp
- Tạo thư mục: ./myweb
- Tạo file ./myweb/index.html (với nội dung là thông tin cá nhân của em)


Tạo file docker-compose.yml để nó sẽ có các dịch vụ sau:
- Khai báo sử dụng nodered/node-red, cổng 1880, dữ liệu nằm tại thư mục ./nodered
- Khai báo sử dụng nginx, cổng 80, cấu hình trong file ./nginx/nginx.conf
- Mount thư mục ./myweb thành thư mục /myweb trong nginx
- Mount file ./nginx/nginx.conf vào file /etc/nginx/nginx.conf trong nginx


Edit file ./nginx/nginx.conf để:
Cấu hình web server cổng 80
server_name là sub-domain (sub-domain tuỳ ý của em)
location / trỏ tới root là thư mục /myweb
location /api dùng proxy_pass trỏ tới 1 (hoặc nhiều) node http_in của nodered

Edit file ./nodered/settings.js để nodered bắt buộc đăng nhập

Chạy docker-compose lần đầu để Node-RED tự sinh file cấu hình trong thư mục ./nodered, sau đó mới tiến hành sửa settings.js và restart lại container
Tiếp theo sinh hash-pw bằng lệnh `docker exec -it nodered node-red admin hash-pw`.

Nó sẽ hỏi password, nhập password bạn muốn (lưu ý: nó không hiện chữ khi nhập)

Sau đó copy paste hash-pw đó vào setting.js, nên chú thích bên cạnh để không quên



**Sau khi xong hết phần C ta được kết quả**
