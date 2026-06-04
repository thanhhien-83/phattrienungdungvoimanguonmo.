## PHÁT TRIỂN ỨNG DỤNG VỚI MÃ NGUỒN MỞ
## HỨA THỊ THANH HIỀN
## K58KTP
## K225480106016
## BÀI TẬP 5

## PHẦN 1. LÝ THUYẾT
# 1. Docker là gì?
Docker là một nền tảng mã nguồn mở cho phép đóng gói, triển khai và chạy các ứng dụng bên trong các môi trường ảo hóa biệt lập gọi là Container.  

- Cách hoạt động: Khác với ảo hóa truyền thống (Virtual Machines - cần cả một hệ điều hành khách OS đầy đủ), Docker Container chia sẻ chung nhân (Kernel) của hệ điều hành máy host.  

- Nó đóng gói ứng dụng cùng tất cả các thư viện, môi trường phụ thuộc (dependencies) đi kèm, đảm bảo ứng dụng chạy đồng nhất ở bất kỳ đâu (từ laptop cá nhân đến máy chủ cloud).

# 2. Các keyword trong docker-compose.yml
Docker-compose là công cụ giúp định nghĩa và quản lý đa container. Dưới đây là các từ khóa cốt lõi chia theo thành phần:

## Cấu trúc tổng thể
- version: Ý nghĩa: Chỉ định phiên bản định dạng cấu trúc của file Docker Compose được sử dụng (ví dụ: '3', '3.8'). Phiên bản này sẽ quyết định các tính năng và cú pháp nào được phép chạy trong file.  

Ví dụ minh họa:  

YAML  
version: '3.8'  

- services:  
Ý nghĩa: Định nghĩa danh sách tất cả các container (dịch vụ) riêng biệt cấu thành nên ứng dụng. Đây là thành phần bắt buộc và quan trọng nhất của file compose.
 
Ví dụ minh họa:  

YAML  
services:  
  nodered:  
    image: nodered/node-red:latest  
    
- networks:
  
Ý nghĩa: Định nghĩa các mạng ảo độc lập ở cấp độ toàn cục. Các mạng này được tạo ra để kết nối hoặc cô lập các nhóm container với nhau.  

Ví dụ minh họa:  

YAML
networks:
  monitor_net:
    driver: bridge
    
- volumes:  
Ý nghĩa: Định nghĩa các vùng lưu trữ dữ liệu bền vững ở cấp độ toàn cục. Các ổ đĩa ảo này tồn tại độc lập với vòng đời của container, giúp dữ liệu không bị mất khi container bị xóa hoặc cập nhật.

Ví dụ minh họa:  

YAML
volumes:
  db_data:

## Các keyword chi tiết trong một service  

Ý nghĩa: Chỉ định Docker Image cụ thể được tải về và sử dụng để khởi tạo container.  

Ví dụ minh họa:  

YAML
image: mariadb:10.6
container_name

Ý nghĩa: Đặt một tên cố định và tường minh cho container khi khởi chạy, giúp em dễ dàng quản lý hoặc gõ lệnh log/inspect thay vì để Docker tự sinh tên ngẫu nhiên.

Ví dụ minh họa:

YAML
container_name: my_flask_api
ports

Ý nghĩa: Thực hiện cấu hình mapping (ánh xạ) cổng từ máy host vật lý vào bên trong mạng cô lập của container theo cấu trúc [Cổng_Máy_Host]:[Cổng_Container].

Ví dụ minh họa:

YAML
ports:
  - "8080:80"
environment

Ý nghĩa: Thiết lập các biến môi trường trực tiếp bên trong container để cấu hình các thông số hệ thống, tài khoản hoặc mật khẩu khi ứng dụng khởi chạy.

Ví dụ minh họa:

YAML
environment:
  - MYSQL_ROOT_PASSWORD=123
volumes

Ý nghĩa: Gắn một thư mục từ máy host hoặc một ổ đĩa ảo (Docker Volume) vào một đường dẫn bên trong container để lưu trữ dữ liệu bền vững, không bị mất đi khi container bị xóa.

Ví dụ minh họa:

YAML
volumes:
  - db_data:/var/lib/mysql
networks

Ý nghĩa: Chỉ định container này sẽ tham gia vào mạng ảo nội bộ nào do Docker Compose khởi tạo, cho phép các container nằm chung mạng dễ dàng giao tiếp qua lại bằng tên của service.

Ví dụ minh họa:

YAML
networks:
  - monitor_network
depends_on

Ý nghĩa: Định nghĩa và thiết lập thứ tự ưu tiên khi khởi chạy giữa các dịch vụ (Ví dụ: quy định container Backend chỉ được phép chạy sau khi container Database đã khởi động xong).

Ví dụ minh họa:

YAML
depends_on:
  - mariadb
restart

Ý nghĩa: Cấu hình chính sách tự động khởi động lại container nếu nó vô tình gặp lỗi dừng đột ngột hoặc khi toàn bộ máy chủ vật lý bị khởi động lại (reboot).

Ví dụ minh họa:

YAML
restart: always
