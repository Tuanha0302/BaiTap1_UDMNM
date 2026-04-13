# G. Triển khai ứng dụng đến End-user
## Tạo tunnel (đường hầm)

Bước 1: Tạo tunnel. Vào Network, chọn Tunnels, chọn Create Tunnel
<img width="960" height="337" alt="cl add tunnel" src="https://github.com/user-attachments/assets/7af545f5-f5ff-448d-8e8d-2fb78afaf011" />

Bước 2: Copy dòng lệnh màu cam, paste vào Ubuntu (tại vị trí ~/myapp)
<img width="960" height="496" alt="kết nối tunnel docker" src="https://github.com/user-attachments/assets/fab26f69-32a4-48aa-9835-6c6234099638" />

Bước 3: Convert sang docker-compose

Trước hết tao tạo file .env để lưu token của cloudflare.

<img width="708" height="117" alt="TOKEN" src="https://github.com/user-attachments/assets/ccbd0154-ff6a-4f9b-bebc-3ea6d2bd63b0" />

Sau đo sử docker-compose.yml như sau, tao không cần phải cho cả token vào đây nữa.

<img width="706" height="341" alt="sua docker yml" src="https://github.com/user-attachments/assets/5eba7e75-1416-4017-a1de-dda38b6258af" />

Bước 4: Cấu hình Public Hostname

<img width="960" height="411" alt="add route" src="https://github.com/user-attachments/assets/d547af54-c0d2-4d50-b6e0-d886453cda75" />

<img width="960" height="436" alt="add route pushlish" src="https://github.com/user-attachments/assets/130b5c0c-5b36-4424-b4d1-0db3e6cdab3e" />

<img width="958" height="540" alt="add ok" src="https://github.com/user-attachments/assets/e530dee1-eeee-4d3b-bf26-fb07d5ba5fe8" />

Bước 5: Cấu hình lại nginx.conf
<img width="704" height="348" alt="sua nginx" src="https://github.com/user-attachments/assets/466160e1-ef02-4e63-ab6b-361ebf3b2163" />

## Kiểm tra url sub-domain đã hoạt động public cho mọi end-user

Để trang web đẹp hơn, em đã sửa code html cho xịn xò hơn. Vậy nên ta được giao diện như này.

<img width="1919" height="1021" alt="image" src="https://github.com/user-attachments/assets/defea325-bad4-4bca-86dd-3a0c363f5a3e" />

