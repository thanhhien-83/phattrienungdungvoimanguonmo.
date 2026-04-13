## phattrienungdungvoimanguonmo.
## A - ĐĂNG KÝ TÊN MIỀN VÀ CLOUDFLARE
# 1. Đăng ký tên miền
Truy cập trang web của iNet và thực hiện đăng ký domain:  
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b22b17ef-d709-4943-9f1c-15f2ccc3cf24" />
Truy cập https://dash.cloudflare.com/sign-up để đăng ký tài khoản. đki thành công  
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e8a4b547-bf75-44b1-853f-db0fa190376d" />
Chọn gói Free ($0):  
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/54f76d6b-3e48-46c3-a86e-0be1e9973d26" />
Cập nhật thành công
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a3890141-e80b-4e29-986e-94e2466a225a" />

## B. Cài đặt Ubuntu + Docker  
1. Cài đặt Ubuntu  
Tải file ISO: truy cập trang ubuntu.com/download/server để tải file .iso của Ubuntu 24.04.4 LTS  
Công cụ giả lập: VMWare
Cài đặt Ubuntu
Sau khi nhấn Power on this virtual machine, màn hình cài đặt của Ubuntu sẽ hiện ra. Thực hiện các bước sau:  
Keyboard Configuration: Chọn English (US).  
Choose type of install: Chọn Ubuntu Server (bản mặc định).  
Networking: Trình cài đặt sẽ tự nhận IP từ VMware qua DHCP. Nhấn Done.  
Storage Configuration: Chọn Use an entire disk.  
Profile Setup:  
Your name: Hien  
Your server's name: hienserver.  
Pick a username: huathanhhien  
Password: 832004  
SSH Setup: Tích chọn Install OpenSSH server.  
Hệ thống sẽ bắt đầu cài đặt. Sau khi hoàn tất chọn Reboot Now.  
<img width="1920" height="1080" alt="Screenshot 2026-04-13 200919" src="https://github.com/user-attachments/assets/3b98e885-76f6-4dd8-9519-09b837120b93" />
đăng nhập với username và password vừa tạo  
<img width="1920" height="1080" alt="Screenshot 2026-04-13 201756" src="https://github.com/user-attachments/assets/a9f16842-c7ff-4259-bddb-ffaa35598cd2" />
Thành công  
<img width="891" height="429" alt="Screenshot 2026-04-13 202116" src="https://github.com/user-attachments/assets/d5d8f3ea-8ecb-4100-a991-f3d35db9939d" />
thực hiện lệnh kiểm tra địa chỉ IP trên Ubuntu Server.
<img width="815" height="155" alt="Screenshot 2026-04-13 202152" src="https://github.com/user-attachments/assets/4071b148-d63a-4787-92e9-d47df5a37ce7" />
Hình này cho thấy việc đăng nhập vào Ubuntu Server qua SSH đã thành công.  
Đã xác nhận bảo mật và nhập xong mật khẩu.  
Hệ thống hiện thông số: RAM dùng 14%, đang chạy bản Ubuntu 24.04.  
Dòng huathanhhien@hienserver:~$ ở cuối nghĩa là server đã sẵn sàng nhận lệnh rồi.  
<img width="1920" height="1080" alt="Screenshot 2026-04-13 202258" src="https://github.com/user-attachments/assets/a14436f3-bd73-4386-8931-569830dc6d8f" />
Thực hiện một loạt các thao tác cơ bản với tệp tin và thư mục trên Linux.  
<img width="1006" height="726" alt="Screenshot 2026-04-13 202959" src="https://github.com/user-attachments/assets/f49249cd-1b5e-483e-a28f-4784463febb8" />
Đã chạy lệnh sudo apt update để cập nhật danh sách gói.  
file tenfile cũng vừa được tạo bằng lệnh nano ở dòng đầu tiên.  
<img width="1581" height="672" alt="Screenshot 2026-04-13 203319" src="https://github.com/user-attachments/assets/30e0ad3b-fe28-4529-ac08-27e34a1db934" />

<img width="1920" height="1080" alt="Screenshot 2026-04-13 203925" src="https://github.com/user-attachments/assets/1736a81a-fefa-4144-88c4-f73c4e63fb5e" />

<img width="907" height="720" alt="Screenshot 2026-04-13 204310" src="https://github.com/user-attachments/assets/9f9644c8-7d82-4eff-830b-4376effb905c" />

<img width="955" height="783" alt="Screenshot 2026-04-13 204609" src="https://github.com/user-attachments/assets/d8dd4b5a-a891-4ae6-9689-81eebc4ebe57" />

## C - CẤU HÌNH DOCKER COMPOSE























