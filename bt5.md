## PHÁT TRIỂN ỨNG DỤNG VỚI MÃ NGUỒN MỞ
## HỨA THỊ THANH HIỀN
## K58KTP
## K225480106016
## BÀI TẬP 5

# PHẦN 1. LÝ THUYẾT
# 1. Docker là gì?
Docker là một nền tảng mã nguồn mở cho phép đóng gói, triển khai và chạy các ứng dụng bên trong các môi trường ảo hóa biệt lập gọi là Container.  

- Cách hoạt động: Khác với ảo hóa truyền thống (Virtual Machines - cần cả một hệ điều hành khách OS đầy đủ), Docker Container chia sẻ chung nhân (Kernel) của hệ điều hành máy host.  

- Nó đóng gói ứng dụng cùng tất cả các thư viện, môi trường phụ thuộc (dependencies) đi kèm, đảm bảo ứng dụng chạy đồng nhất ở bất kỳ đâu (từ laptop cá nhân đến máy chủ cloud).

# 2. Các keyword trong docker-compose.yml
Docker-compose là công cụ giúp định nghĩa và quản lý đa container. Dưới đây là các từ khóa cốt lõi chia theo thành phần:

## Cấu trúc tổng thể
- version:  
Ý nghĩa: Chỉ định phiên bản định dạng cấu trúc của file Docker Compose được sử dụng (ví dụ: '3', '3.8'). Phiên bản này sẽ quyết định các tính năng và cú pháp nào được phép chạy trong file.   

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

# 2.1. CÁC KEYWORD CHI TIẾT TRONG MỘT SERVICE (CONTAINER)
- image  
Ý nghĩa: Chỉ định Docker Image cụ thể được tải về từ Docker Hub (hoặc một Registry riêng) để khởi tạo nên container đó.  
Ví dụ minh họa:  

YAML
image: mariadb:10.6

- build  
Ý nghĩa: Dùng khi ứng dụng là mã nguồn tự viết (như Flask API trong bài). Thay vì tải image có sẵn, Docker sẽ tìm đến thư mục chứa file Dockerfile để tự đóng gói thành image mới.  
Ví dụ minh họa:  

YAML
build: ./backend

- container_name  
Ý nghĩa: Đặt một tên cố định và tường minh cho container khi khởi chạy, giúp em dễ dàng quản lý, kiểm tra logs hoặc gõ lệnh trực tiếp trong terminal thay vì để Docker tự sinh tên ngẫu nhiên.  
Ví dụ minh họa:  

YAML
container_name: monitor_nginx

- ports  
Ý nghĩa: Thực hiện cấu hình mapping (ánh xạ) cổng từ máy host vật lý vào bên trong mạng cô lập của container theo cấu trúc [Cổng_Máy_Host]:[Cổng_Container].  
Ví dụ minh họa:  

YAML
ports:
   "80:80"

- environment  
Ý nghĩa: Thiết lập các biến môi trường trực tiếp bên trong container để cấu hình các thông số hệ thống, tài khoản, tên cơ sở dữ liệu hoặc mật khẩu khi ứng dụng khởi chạy.  
Ví dụ minh họa:  

YAML
environment:
- ./frontend:/usr/share/nginx/html
    
- volumes  
Ý nghĩa: Gắn một thư mục từ máy host hoặc một ổ đĩa ảo (được định nghĩa ở mục toàn cục) vào một đường dẫn bên trong container để lưu trữ dữ liệu lâu dài hoặc chia sẻ file code.  
Ví dụ minh họa:  

YAML
volumes:
  - ./frontend:/usr/share/nginx/html

- networks  
Ý nghĩa: Chỉ định container này sẽ tham gia vào mạng ảo nội bộ nào (trong số các mạng đã định nghĩa ở phần networks toàn cục), giúp các container kết nối giao tiếp được với nhau.  
Ví dụ minh họa:

YAML
networks:
  - monitor_net

- depends_on  
Ý nghĩa: Định nghĩa và thiết lập thứ tự ưu tiên khi khởi chạy giữa các dịch vụ (ví dụ: quy định container Grafana chỉ được phép khởi động sau khi container InfluxDB đã chạy xong).  
Ví dụ minh họa:

YAML
depends_on:
  - influxdb
    
- restart  
Ý nghĩa: Cấu hình chính sách tự động khởi động lại container nếu nó vô tình gặp lỗi dừng đột ngột hoặc khi toàn bộ máy chủ vật lý bị khởi động lại (reboot).  
Ví dụ minh họa:

YAML
restart: always
# 2.2. CÁC KEYWORD CHI TIẾT TRONG NETWORKS (MẠNG ẢO)
- driver  
Ý nghĩa: Chỉ định loại driver mạng ảo sẽ sử dụng. Phổ biến nhất là bridge (tạo mạng cầu nối nội bộ trên một máy host) hoặc overlay (nếu chạy đa máy chủ với cấu trúc phức tạp).  
Ví dụ minh họa:

YAML
driver: bridge
- external  
Ý nghĩa: Nếu đặt là true, Docker Compose sẽ không tự tạo ra mạng mới khi khởi chạy mà sẽ tìm và kết nối các container vào một mạng ảo đã được người dùng tạo thủ công từ trước bằng lệnh bên ngoài.  
Ví dụ minh họa:

YAML
external: true
# 2.3. CÁC KEYWORD CHI TIẾT TRONG VOLUMES (Ổ ĐĨA LƯU TRỮ)
- driver  
Ý nghĩa: Chỉ định driver quản lý lưu trữ dữ liệu. Mặc định hệ thống sử dụng local (lưu trực tiếp trên ổ cứng của máy host), nhưng có thể mở rộng sang các driver lưu trữ đám mây hoặc ổ đĩa mạng tập trung.  
Ví dụ minh họa:

YAML
driver: local
- driver_opts  
Ý nghĩa: Định nghĩa các tham số tùy chọn nâng cao đi kèm cho driver volume nhằm can thiệp sâu vào cấu hình hệ thống (như thiết lập kiểu mount, quyền hạn truy cập hoặc gán cứng vào một thư mục vật lý cụ thể).  
Ví dụ minh họa:

YAML
driver_opts:
  type: "none"
  o: "bind"
  device: "/home/user/data"

# 3. Ưu điểm khi triển khai ứng dụng sử dụng Docker
- Tính nhất quán (Consistency): Giải quyết triệt để lỗi kinh điển "Chạy trên máy em ngon lành nhưng lên máy chủ lại lỗi". Môi trường dev, test, và production là y hệt nhau.

- Nhẹ và Hiệu năng cao (Lightweight): Container khởi động trong vài giây, tốn ít RAM/CPU hơn rất nhiều so với máy ảo VM vì không phải gánh cả HĐH riêng.

- Dễ dàng quản lý & Cô lập (Isolation): Mỗi ứng dụng chạy trong không gian riêng, lỗi của container này không ảnh hưởng đến container khác hoặc máy host.

- Mở rộng nhanh chóng (Scalability): Dễ dàng nhân bản (scale) tăng số lượng container lên khi lượng truy cập tăng.
