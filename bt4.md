## Môn: Phát triển ứng dụng với mã nguồn mở-TEE0421
## Hứa Thị Thanh Hiền
## Lớp: 58KTPM
# Bài tập 04:

## KHAI THÁC N8N ĐỂ TỰ ĐỘNG ĐĂNG BÀI LÊN WORDPRESS
deadline : 23h59 ngày 25 tháng 5 năm 2026.
SỬ DỤNG KẾT QUẢ ĐÃ LÀM Ở BÀI TẬP 3, BỔ SUNG VÀO DOCKER COMPOSE ĐỂ CÓ THÊM SERVICE 8N8:
1. Cấu hình các file trong dokcer-compose.yml:  

- Mariadb:  

image

- PhPAdmin:  
image

- WordPress:  
image

- Cấu hình Tunel cloudflare để truy cập vào các dịch vụ bằng các subdomain ( em sử dụng lệnh cli thay cho việc thao tác đồ họa trên dashboard của cloudflare):  

- Tạo tunel của 3 sub-domain:  
image
image

- Thêm chuỗi id tunel vào config.yml:  
image
- Cấu hình dịch vụ cloudflare trong docker-compose.yml:  
image
- Cấp lại quyền truy cập file trên máy host:  
image
- n8n:
image

- Pull các images về và chạy chúng:  
image
2. Kiểm tra truy cập các sub-domain:   
- Truy cập sub-domain2 để quan sát xem cơ sở dữ liệu chưa có bảng nào:  
image
- Truy cập sub-domain1 để cài đặt wordpress:  
image
- Truy cập sub-domain2 để quan sát xem cơ sở dữ liệu có những bảng dữ liệu nào sau khi cài wp:  
image
- Tạo 1 bài viết trong wordpress giới thiệu về bản thân sinh viên: thông tin cá nhân, sở thích, ... bài viết có thể chứa hình ảnh, âm thanh, video, ...  
image
- Tạo 1 bài viết trong wordpress giới thiệu về nhữn kiến thức mà em đã học được ở môn Phát triển ứng dụng với mã nguồn mở  
image
- Truy cập sub-domain3 để cấu hình n8n:  
tạo tài khoản admin :  
image
3. Cấu hình n8n:  
- Send me a Licence key:  
image

- Kiểm tra email:  
image

- Activate License key: ( trang chủ -> setting -> usage and plan -> enter activation key -> điền key vừa nhận từ email vào):  
image

- Tạo workflow mới:  
image

- Add trigger node: tìm node: Telegram => OnMessage ; cấu hình Credential: Set up Credential => cần Nhập Access Token  

- Cần chát với bot @BotFather trên Telegram để đẻ ra bot mới của riêng mình:  
image
- Sau khi tạo bot mới cần copy lấy Token  
image
image
- Chát lần đầu với bot mới này:  
image
image
- Add (nối tiếp vào sau node Telegram Trigger) node: AI Google Gemini => Message a model => Set up Credential => cần Nhập API KEY  

- Lấy API KEY tại trang: https://aistudio.google.com  
image

- Nhập API Key lên giao diện n8n:  
image

- kéo thả nội dung đã chát với bot của telegram (phía bên trái) vào nội dung phần PROMPT kết quả được {{ $json.message.text }}, cần gõ thêm vào sau {{ $json.message.text }} để promt dài hơn : vd ({{   $json.message.text }}. Kết quả sinh ra ở định dạng HTML+CSS để tôi dùng HTML+CSS này tạo bài viết cho wordpress.)  
image

- Turn on Output Content as JSON : để kết quả trả về dạng json  
image

- Thêm Option để AI viết bài thông minh hơn, văn phong nhiều màu hơn thay vì những văn bản chứa các nội dung cứng ngắc:  
image

- Add (nối tiếp vào sau node Message a model) node: Code in JavaScript  
image

- Add (nối tiếp vào sau node Code in JavaScript) node: WordPress => Create a Post  

- Set up Credential: vào wp tại url: https://sub-domain1/wp-admin => vào mục Tài Khoản => chọn user đã tạo lúc setup wordpress => Mật khẩu ứng dụng => Nhập n8n và bấm "Thêm mật khẩu ứng dụng" => copy chuỗi   24 kí tự : Đây là mật khẩu ứng dụng => paste vào mục Password của n8n Credential  
image
image

- Quay lại n8n:  
image

- Cấu hình node Create a Post: bấm nút Execute previous nodes sau đó thực hiện các bước trong ảnh:  
image

- PUBLISH flow (góc trên phải) Nút này thực hiện việc xuất bản flow <=> flow sẽ tự động thực thi khi thoả mãn điều kiện trigger  
image

4. Kết quả: 
5. Nhận xét kết quả đạt được:  
Triển khai thành công Stack dịch vụ mã nguồn mở gồm MariaDB, phpMyAdmin, WordPress và n8n chạy biệt lập trên môi trường Docker. Kết nối HTTPS qua Cloudflare Tunnel hoạt động ổn định.  
Tự động hóa hoàn chỉnh: Xây dựng thành công luồng dữ liệu khép kín tự động 24/7: Người dùng nhắn tin (Telegram Bot) ➔ Trí tuệ nhân tạo (Google Gemini AI) xử lý & sinh cấu trúc JSON/HTML ➔ Code   JavaScript dọn dẹp, xử lý chuỗi ➔ Tự động xuất bản bài viết (WordPress API).  

Tối ưu hóa và Xử lý lỗi: Hệ thống được cấu hình System Message chặt chẽ giúp ép văn phong chuẩn xác hơn, xử lý chuỗi bằng JavaScript giúp hệ thống vận hành mượt mà.  
