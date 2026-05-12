## Môn: Phát triển ứng dụng với mã nguồn mở-TEE0421
## Lớp: 58KTPM
## Tên: Hứa Thị Thanh Hiền
## Mssv: 
## Bài tập 03:

SỬ DỤNG WEB SITE WORDPRESS ĐỂ TẠO  
- Tạo 1 bài viết trong wordpress giới thiệu về bản thân sinh viên: thông tin cá nhân, sở hữu, ... bài viết có thể chứa hình ảnh, âm thanh, video, ...  
- Tạo 1 bài viết trong wordpress giới thiệu về các ngành học mà em yêu thích trong trường TNUT.  
thời hạn: 23h59 ngày 12 tháng 5 năm 2026.  

- Cấu hình Docker Compose: tạo một thư mục dự án để quản lý các file, sau đó tạo file cấu hình

<img width="1472" height="772" alt="1" src="https://github.com/user-attachments/assets/fb654be2-35c9-47a4-991b-aff851382ac9" />

- Dán nội dung sau vào file
  
<img width="1918" height="1078" alt="2" src="https://github.com/user-attachments/assets/0c27d08c-f593-479d-a2ad-9306e2f22eb2" />
- Chạy thành công
  
<img width="1920" height="1080" alt="3" src="https://github.com/user-attachments/assets/c8500f76-6034-4efc-b91b-3173475e2cbe" />

- Thiết lập tài khoản quản trị WordPress tại localhost:8000, với tên người dùng là huathanhhien và tên website là Hienxinhiu.
  
<img width="1920" height="1080" alt="4" src="https://github.com/user-attachments/assets/1c3a763e-1f6a-4c69-9b6b-8b6dc1e6b11e" />

- Giao diện phpMyAdmin chạy tại localhost:8080, xác nhận đã kết nối thành công với máy chủ MariaDB và cơ sở dữ liệu wordpress_db đã sẵn sàng.
  
<img width="1920" height="1080" alt="5" src="https://github.com/user-attachments/assets/320dfe52-5ab5-4009-aadd-3b2a831541cc" />

- Giao diện Trang quản trị (Dashboard) của WordPress sau khi cài đặt thành công, nơi bắt đầu quản lý nội dung, thay đổi giao diện và cài đặt các plugin cho website.
  
<img width="1920" height="1080" alt="6" src="https://github.com/user-attachments/assets/3ce94350-c70a-4215-92f3-3d3fb626c451" />

- Vào mục Bài viết (Posts) và sẵn sàng để viết bài. Dưới đây là nội dung mẫu cho bài đăng thứ nhất giới thiệu về bản thân sinh viên.
  
<img width="1920" height="1080" alt="7" src="https://github.com/user-attachments/assets/85d89d64-326e-4b41-a0e6-9ae474b98dfb" />

- Nội dung bài đăng thứ 2

<img width="1920" height="1080" alt="8" src="https://github.com/user-attachments/assets/f9fb8d97-dc43-4ac6-bd96-79e98fc5c50a" />

- Lệnh này có tác dụng tải file cài đặt .deb của cloudflared từ GitHub để chuẩn bị cho bước đưa website của lên internet (public qua tunnel).
  
<img width="1918" height="310" alt="9" src="https://github.com/user-attachments/assets/e2187b06-ad3e-45ea-8a73-cb78aefcf1db" />

- Lệnh này đã giải nén và thiết lập trình điều khiển Cloudflare Tunnel lên máy tính. Hệ thống báo Setting up cloudflared (2026.3.0) nghĩa là việc cài đặt đã hoàn tất thành công.
  
<img width="1918" height="280" alt="10" src="https://github.com/user-attachments/assets/5eb66833-36ae-47cf-b770-e05e3c356fa9" />

- Giao diện phpMyAdmin hiển thị cấu trúc bên trong của cơ sở dữ liệu wordpress_db sau khi em đã cài đặt xong WordPress.
  
- WordPress đã tự động tạo ra 12 bảng dữ liệu (như wp_posts, wp_users, wp_comments...) để lưu trữ toàn bộ nội dung bài viết, tài khoản và cài đặt của website.

<img width="1920" height="1080" alt="11 csdl" src="https://github.com/user-attachments/assets/aa154e1d-6f99-40e0-ae97-cf30194b4f7e" />

- Đây là giao diện bên trong của bảng wp_posts trong cơ sở dữ liệu, nơi lưu trữ toàn bộ các bài viết em vừa tạo.
  
- Dòng số 5 & 8: Đã có bài viết về "Giới thiệu bản thân".

- Dòng số 10 & 12: Đã có bài viết về "Ngành học em yêu thích tại TNUT - Kỹ thuật Máy tính".
<img width="1920" height="1080" alt="12" src="https://github.com/user-attachments/assets/15c83a2d-775e-4dde-8cfb-26daeb05b41d" />

<img width="1918" height="926" alt="13" src="https://github.com/user-attachments/assets/afe0c6bd-bf62-4b07-a0f2-b5b8958c8063" />

<img width="895" height="142" alt="14" src="https://github.com/user-attachments/assets/22305aef-93f4-47b1-a11b-759af3830b70" />

<img width="1908" height="202" alt="15" src="https://github.com/user-attachments/assets/a8ada83c-906a-4b15-a5b4-baf44be5aff9" />

<img width="1917" height="237" alt="16" src="https://github.com/user-attachments/assets/868f084a-7a6d-4f83-a844-72a5e60c875b" />

<img width="1920" height="1080" alt="17" src="https://github.com/user-attachments/assets/f7eef95a-c583-4004-b4de-d53d7b61d1e3" />

<img width="1920" height="1080" alt="18" src="https://github.com/user-attachments/assets/891a0d72-10c9-43cf-b321-a2d8c48ff468" />


















