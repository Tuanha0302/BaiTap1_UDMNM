# G. Câu hỏi về bài làm

## 1. Tại sao dùng Nginx làm Reverse Proxy?

- Tunnel chỉ là đường hầm → cần 1 server nhận request
- Nginx làm gateway (entrypoint)

**Ưu điểm:**
- Phân luồng (`/`, `/api`)
- Ẩn backend (Node-RED)
- Dễ mở rộng hệ thống
- Tăng bảo mật

**Nếu trỏ thẳng Node-RED:**
- Lộ backend
- Khó mở rộng
- Không tách frontend/backend

---

## 2. Mount file vs Mount thư mục

**Mount file**
- Ví dụ: ./nginx/nginx.conf:/etc/nginx/nginx.conf
- Dùng cho config
- Kiểm soát chính xác

**Mount thư mục**
- Ví dụ: ./myweb:/myweb
- Dùng cho code, data
- Sửa ngoài → update ngay

---

## 3. Sửa index.html có cập nhật ngay không?

- Có

**Vì:**
- Thư mục đã mount vào nginx
- File thay đổi → nginx đọc lại ngay
- Không cần restart

---

## 4. restart: always vs unless-stopped

- always: luôn restart (kể cả reboot)
- unless-stopped: giống nhưng stop tay → không restart

→ Giúp service tự chạy lại khi lỗi

---

## 5. Dùng chung network

**Khai báo:**
- networks:
  - mynetwork:
    - driver: bridge

**Gán cho service:**
- nginx → mynetwork
- nodered → mynetwork
- myapi → mynetwork
- cloudflared → mynetwork

**Lợi ích:**
- Gọi nhau bằng tên (myapi:9630)
- Tách biệt mạng ngoài
- Dễ quản lý, bảo mật hơn

---

## 6. Vì sao dùng .env và không push lên GitHub?

- .env chứa token, API key

**Nếu lộ:**
- Bị chiếm quyền tunnel
- Rò rỉ dữ liệu

→ Phải thêm .env vào .gitignore

---

## 7. Tại sao thêm :ro?

- :ro = chỉ đọc

**Lợi ích:**
- Tránh sửa config từ container
- Tăng bảo mật

---

## 8. Dùng Tunnel có cần mở port không?

- Không cần mở port cho backend

**Luồng:**
- User → Tunnel → Nginx → Backend

→ Backend không bị expose ra ngoài
