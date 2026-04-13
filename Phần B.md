# B. Cài đặt Ubuntu + Docker
## Cài đặt hệ điều hành Ubuntu 24.04.4 LTS
### Sử dụng một trong các công cụ để giả lập: Dùng VirutualBox (Miễn phí).

Đầu tiên, cần tải VirutualBox bằng link: https://www.oracle.com/latam/virtualization/technologies/vm/downloads/virtualbox-downloads.html

Cài đặt và mở nó lên.

Tải file iso của ubuntu: https://releases.ubuntu.com/24.04.4/ubuntu-24.04.4-live-server-amd64.iso

Rồi, ta bắt đầu tạo máy ảo: làm theo các bước:

<img width="596" height="407" alt="new ub 1" src="https://github.com/user-attachments/assets/fc6e8803-8bbc-40a7-b354-07012a356537" />

<img width="596" height="413" alt="new ub 2" src="https://github.com/user-attachments/assets/600cc27f-0be1-483a-9d29-1b6875d33e37" />

<img width="598" height="411" alt="new ub 3" src="https://github.com/user-attachments/assets/490607ef-5403-4a14-877b-3987bb02a2f8" />

<img width="594" height="415" alt="new ub 4" src="https://github.com/user-attachments/assets/30cea161-cc3d-4afc-a79f-5a0c85fab5a2" />

Sau khi cài xong thì máy ảo sẽ tự chạy, Ta chờ nó chạy xong các thiết lập ban đầu rồi reboot:

<img width="637" height="442" alt="chờ setup ban đầu" src="https://github.com/user-attachments/assets/da8707b9-0085-4b42-9488-de0074302964" />

<img width="636" height="435" alt="reboot" src="https://github.com/user-attachments/assets/b56f6978-9097-450e-ab42-0a09af5a36fc" />

Sau khi reboot, login theo đúng username và password đã thiết lập khi tạo máy ảo

<img width="640" height="410" alt="login ok" src="https://github.com/user-attachments/assets/69f87377-50aa-42c4-85af-3cd21be8d476" />

Sau đó, tắt máy ảo để thiết lập mạng.

### Cấu hình mạng trong Ubuntu (và công cụ giả lập) để cho phép truy cập SSH vào Ubuntu từ cmd của windows

Trước hết, thiết lập cho virtualbox, tắt dhcp cho host-only để tý ta sẽ đặt ip tĩnh. Sau đố tạo nat network.

<img width="541" height="478" alt="off dhcp" src="https://github.com/user-attachments/assets/225b5d38-1dc5-439f-be87-ea8ce19b0239" />

<img width="541" height="453" alt="create nat" src="https://github.com/user-attachments/assets/07442b04-f3d1-4f22-b8d9-b4f3a7465042" />

Tiếp theo thiết lập mạng cho ubuntu, thiết lập cho 2 adapter để 1 cái thông với internet, 1 cái để máy khác ssh vào.

<img width="579" height="284" alt="st ap1 nat" src="https://github.com/user-attachments/assets/f4d8c404-ed1d-41a6-9942-ce1e8e28123b" />

<img width="587" height="306" alt="st ap2 host" src="https://github.com/user-attachments/assets/c3029907-84c3-476d-807d-05aba8f29c59" />

Sau đo, thiết lập ip tĩnh. Chạy ubuntu, chạy lệnh `sudo nano /etc/netplan/*.yaml` và thiết lập enp0s8 như hình, rồi dùng lệnh `sudo netplan apply` để cấu hình có hiệu lực.

<img width="639" height="184" alt="netplan" src="https://github.com/user-attachments/assets/f454d819-0caf-49db-b51c-9e11ca18e3f3" />

Ta check ip thấy nhưu này là ok.

<img width="640" height="103" alt="ip" src="https://github.com/user-attachments/assets/6942a334-9c29-45cf-9d7d-9cd8c842ff2c" />

Tiếp theo tải ssh bằng lệnh `sudo apt install openssh-server -y`. 

<img width="647" height="259" alt="sudo apt update" src="https://github.com/user-attachments/assets/e6c2ebcc-ea18-4175-8dd7-94717e4acfe7" />

<img width="662" height="441" alt="ssh server" src="https://github.com/user-attachments/assets/467a92d0-feda-47d5-a5f9-96c0b92115e1" />

Sau khi cài xong ssh, mở cmd của windows, dùng `ssh tuanha@192.168.56.20`

<img width="670" height="371" alt="ssh ok" src="https://github.com/user-attachments/assets/d627367b-48c8-4c63-9ab0-a0402a62cc61" />

## Tìm hiểu các lệnh cơ bản của ubuntu
Các lệnh cần tìm hiểu:

- Liệt kê các file trong thư mục: ls
- Tạo thư mục: mkdir nameFolder
- Chuyển thư mục làm việc: cd path
- Copy file: cp file_nguồn path/file_đích
- Thay đổi quyền thao tác file: sudo chmod xxx filename
- Edit file: sudo nano tenfile
- CTRL+o : lưu nội dung sau khi edit
- CTRL+x : thoát edit file
- Xem ip của máy ubuntu: ip -4 addr

Test vài lệnh;

<img width="673" height="245" alt="test lenh" src="https://github.com/user-attachments/assets/5703d5f1-084b-4c87-9634-46a515ec2f21" />

## Cài đặt docker cho Ubuntu

Tiếp theo ta tải docker và docker compose.

<img width="651" height="134" alt="i docker" src="https://github.com/user-attachments/assets/20e3e1ae-3435-488a-b302-6199369866e0" />

<img width="651" height="186" alt="i docker compose" src="https://github.com/user-attachments/assets/89ceb37c-7d15-4fa2-a3c4-071e4ae55b4b" />

Ta kiểm tra phiên bản vừa tải.

<img width="616" height="70" alt="check version" src="https://github.com/user-attachments/assets/05c03ae3-4c91-46ab-8f3e-c278d8855466" />

Ta cập nhật quyền sở hữu để không phải dùng sudo cho các lệnh docker. 

<img width="664" height="37" alt="usernod" src="https://github.com/user-attachments/assets/ba31bd9f-da52-4f83-b231-ea708e9eef30" />

Sau khi thiết lập xong, tắt cmd và mở lại, ssh lại vào ubuntu để check.

<img width="667" height="76" alt="test docker" src="https://github.com/user-attachments/assets/8d60d741-40fc-4f5f-ad7f-46375a7aa62d" />

ok. giờ mở port

<img width="662" height="131" alt="allow port" src="https://github.com/user-attachments/assets/d928c57d-dff2-4efa-85c7-db30fa649f33" />

