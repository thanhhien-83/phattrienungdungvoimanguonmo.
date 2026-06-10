## PHÁT TRIỂN ỨNG DỤNG VỚI MÃ NGUỒN MỞ
## HỨA THỊ THANH HIỀN
## K58KTP
## K225480106016
## BÀI TẬP 5

# ĐỀ BÀI
## Lý thuyết:
Docker là gì?

Các keyword được sử dụng trong docker-compose.yml

Để mô tả 1 service, network, volume,...

Liệt kê + ý nghĩa của từ khoá đó + ví dụ minh hoạ

Ưu điểm khi triển app sử dụng docker là gì?

Dùng docker: tạo app, test app OK trên laptop cá nhân

Giờ muốn triển khai app này trên máy chủ thật ko có internet thì các bước cần làm là?

## Thực hành áp dụng: APP MONITOR + ALERT DATA REALTIME
Sử dụng docker compose có nhiều serivce

Và các thành phần cần thiết để tạo thành ứng dụng:

Nodered liên tục lấy dữ liệu từ nguồn nào đó (chứng khoán, thời tiết, giá vàng,...) nguồn thực tế, số liệu luôn động sau thời gian ngắn

Nodered lưu trữ dữ liệu vào 2 database: mariadb để lưu giá trị tức thời, lưu lịch sử vào influxdb

Sử dụng grafana để trực quan hoá dữ liệu: vẽ biểu đồ
Sử dụng nginx để làm webserver

Chạy 1 trang web html+js+css làm front-end

js: lấy dữ liệu tức thời trong mariadb qua (ajax | socket)

Gọi api (api tự build bằng Flask giống bt1

Api trả về giá trị tức thời trong mariadb

Hiển thị lên web, auto hiển thị số mới khi thay đổi

Sử dụng iframe để gọi grafana

Hiển thị biểu đồ dữ liệu lịch sử của thông số đã lưu

Quan sát dữ liệu lịch sử => Giá trị bất thường (VD MIỀN A..B: OK, DƯỚI A: ALERT LOW, TRÊN B: ALERT HIGH)

Nodered: kết hợp bot Telegram

Khi dữ liệu not OK, thì gửi tin nhắn từ bot => group trên telegram

Group đã add bot vào: (nhóm đã có 2 người), add thêm 1875746636 thành 3 người

Mỗi khi bot gửi dữ liệu vào nhóm: mọi member of group đều nhận đc

Nội dung alert: tường minh, có value gây alert

Xuất tất cả các container ra file nén.

Xoá mọi container đang chạy

Load lại các container từ file nén để khôi phục các container đã xoá.


# PHẦN 1. LÝ THUYẾT
# 1. Docker là gì?
Docker là một nền tảng mã nguồn mở cho phép đóng gói, triển khai và chạy các ứng dụng bên trong các môi trường ảo hóa biệt lập gọi là Container.  

- Cách hoạt động: Khác với ảo hóa truyền thống (Virtual Machines - cần cả một hệ điều hành khách OS đầy đủ), Docker Container chia sẻ chung nhân (Kernel) của hệ điều hành máy host.  

- Nó đóng gói ứng dụng cùng tất cả các thư viện, môi trường phụ thuộc (dependencies) đi kèm, đảm bảo ứng dụng chạy đồng nhất ở bất kỳ đâu (từ laptop cá nhân đến

 máy chủ cloud).

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

# Dưới đây là các bước chi tiết, tường minh để triển khai ứng dụng từ laptop cá nhân lên máy chủ thật không có kết nối internet (quy trình Offline Deployment):

## BƯỚC 1: ĐÓNG GÓI CÁC DOCKER IMAGES TẠI MÁY CÁ NHÂN (NƠI CÓ INTERNET)

Sau khi đã khởi chạy và kiểm thử ứng dụng chạy ổn định trên laptop, em tiến hành gom tất cả các Docker Image có trong file docker-compose.yml và nén lại thành một file .tar duy nhất.  

Mở Terminal tại laptop và chạy câu lệnh sau:  

Bash
docker save -o monitor_app_images.tar mariadb:10.6 influxdb:1.8 nodered/node-red:latest grafana/grafana:latest nginx:latest monitor_flask_api:latest  

Ý nghĩa: Lệnh này sẽ xuất (save) danh sách các image được chỉ định thành một file nén có tên là monitor_app_images.tar.  

## BƯỚC 2: CHUẨN BỊ VÀ SAO CHÉP MÃ NGUỒN SANG THIẾT BỊ LƯU TRỮ

Em sao chép toàn bộ các thư mục cấu hình và file nén image vào một thiết bị lưu trữ ngoại vi (USB hoặc ổ cứng di động). Các file cần copy bao gồm:  

File nén image: monitor_app_images.tar vừa tạo ở Bước 1.  

File cấu hình hệ thống: docker-compose.yml.  

Các thư mục chứa mã nguồn hoặc cấu hình tĩnh: Thư mục frontend/ (chứa file index.html) và thư mục backend/ (chứa app.py, Dockerfile nếu cần lưu trữ lại cấu hình build).  

## BƯỚC 3: CÀI ĐẶT DOCKER OFFLINE TRÊN MÁY CHỦ THẬT

Vì máy chủ không có internet, em không thể dùng lệnh apt-get install hay yum install thông thường.  

Tại máy có mạng, truy cập vào trang chủ Docker để tải về file cài đặt offline (gói .deb đối với Ubuntu/Debian hoặc .rpm đối với CentOS/RHEL) cùng với file thực thi của docker-compose.  

Copy các file cài đặt này qua USB sang máy chủ.  

Tại máy chủ, tiến hành cài đặt các gói bằng lệnh cài đặt local:  

Đối với Ubuntu: sudo dpkg -i đường_dẫn_file.deb  

Đối với CentOS: sudo rpm -i đường_dẫn_file.rpm  

Cấp quyền thực thi cho docker-compose: sudo chmod +x /usr/local/bin/docker-compose  

## BƯỚC 4: NẠP (LOAD) CÁC DOCKER IMAGES VÀO MÁY CHỦ

Cắm USB vào máy chủ thật, sao chép toàn bộ các file dự án vào một thư mục làm việc (ví dụ: /home/user/app_monitor).  

Mở Terminal của máy chủ, di chuyển vào thư mục chứa file .tar và thực hiện lệnh nạp image:  

Bash
docker load -i monitor_app_images.tar

Ý nghĩa: Docker sẽ giải nén file monitor_app_images.tar và nạp toàn bộ các image vào kho lưu trữ cục bộ (Local Registry) của máy chủ. Em có thể kiểm tra lại bằng lệnh docker images.  

## BƯỚC 5: KHỞI CHẠY HỆ THỐNG TRÊN MÁY CHỦ KHÔNG CÓ MẠNG

Tại Terminal của máy chủ, di chuyển vào đúng thư mục chứa file docker-compose.yml và các thư mục code đi kèm, sau đó gõ lệnh khởi chạy:  

Bash
docker-compose up -d

Ý nghĩa: Docker Compose sẽ đọc cấu hình trong file yaml, tự động nhận diện các image đã được nạp sẵn ở Bước 4 (mà không cần lên Docker Hub tải về) để tạo các mạng ảo, ổ đĩa ảo và thiết lập các container chạy ngầm (-d) hoàn chỉnh.  

# Phần 2: Thực hành 
## 2.1 Kiểm tra trạng thái container

- Kiểm tra trạng thái container (1.png): Sử dụng công cụ quản lý Docker để kiểm tra chi tiết danh sách, cổng ánh xạ mạng và đảm bảo cả 5 container thành phần đều đang chạy ổn định, dùng lệnh sudo docker ps.

<img width="1611" height="292" alt="1" src="https://github.com/user-attachments/assets/eb365fec-d2cc-4aef-a61e-0147fed13974" />

## 2.2. Tạo docker-compose.yml

- Cấu hình tham số môi trường: Thiết lập cổng mạng kết nối, tài khoản mật khẩu root và phân vùng lưu trữ cho dịch vụ cơ sở dữ liệu MariaDB cùng InfluxDB, dùng lệnh nano docker-compose.yml.
  
<img width="737" height="632" alt="2" src="https://github.com/user-attachments/assets/554db753-bdfb-425c-a5a5-f74b711bf4a1" />

## 2.3. Xây dựng dịch vụ Backend API

- Lập trình mã nguồn Flask: Xây dựng ứng dụng Python thiết lập kết nối cơ sở dữ liệu MariaDB và định nghĩa hàm truy vấn lấy ra giá trị giá vàng mới nhất, dùng lệnh nano flask-api/app.py.
  
<img width="1105" height="633" alt="3" src="https://github.com/user-attachments/assets/42dc4ed4-3628-45e9-b494-d7bb2e34b3e8" />

- Khai báo thư viện phụ thuộc: Liệt kê danh sách các gói công cụ cài đặt bắt buộc cho môi trường hoạt động của ứng dụng Backend bao gồm Flask và thư viện kết nối cơ sở dữ liệu, dùng lệnh nano flask-api/requirements.txt.
  
<img width="1098" height="184" alt="4" src="https://github.com/user-attachments/assets/d5dae65c-8590-4c30-8d23-4309ba8a625b" />

- Đóng gói môi trường chạy: Khởi tạo kịch bản đóng gói ảnh hệ thống Docker độc lập dựa trên nền tảng môi trường Python phiên bản 3.11, dùng lệnh nano flask-api/Dockerfile.
  
<img width="741" height="292" alt="5" src="https://github.com/user-attachments/assets/6e7beec7-c6f6-46aa-a439-8bf3c4d74f85" />

## 2.4. Xây dựng giao diện Front-end

- Tạo trang chủ Dashboard: Thiết lập cấu trúc hiển thị trang web tĩnh cho người theo dõi và cấu hình thẻ iframe liên kết nhúng biểu đồ động từ Grafana, dùng lệnh nano nginx/html/index.html.
  
<img width="1103" height="632" alt="6" src="https://github.com/user-attachments/assets/41ad5a99-0e6b-485b-8bf8-e611d86c9d6a" />

- Lập trình luồng Ajax Realtime: Viết hàm JavaScript chạy ngầm thực hiện tự động gửi yêu cầu lấy số liệu giá vàng mới nhất từ Flask API theo chu kỳ lặp lại mỗi 5 giây, dùng lệnh nano nginx/html/script.js.
  
<img width="1005" height="560" alt="7" src="https://github.com/user-attachments/assets/556c47f6-0f47-4ffe-9239-dadf70c37fe9" />

- Cấu hình máy chủ Nginx: Thiết lập cổng mạng lắng nghe công khai và ánh xạ điều hướng luồng dữ liệu truy cập cổng hệ thống /api/ kết nối trực tiếp về container Flask, dùng lệnh nano nginx/nginx.conf.

<img width="969" height="568" alt="8" src="https://github.com/user-attachments/assets/50ed463d-9406-4ac5-87ec-0be5e6e8b18f" />

## 2.5. Khởi chạy hệ thống
-  Kích hoạt dự án đa dịch vụ: Khởi chạy đồng bộ tổ hợp tất cả các dịch vụ chạy ngầm dưới nền và kiểm tra danh sách trạng thái hoạt động thực tế của các container, dùng lệnh sudo docker-compose up -d và sudo docker ps.
  
<img width="1494" height="283" alt="9" src="https://github.com/user-attachments/assets/499fe2d0-613c-43ff-ae2f-90c3c64cfdc3" />

  ## 2.6. Quản trị Cơ sở dữ liệu MariaDB
  
- Kiểm tra bảng và chèn dữ liệu mẫu: Thực hiện kết nối vào hệ quản trị cơ sở dữ liệu để kiểm tra trạng thái bảng trống và chạy lệnh chèn thử nghiệm một bản ghi giá vàng mới, dùng lệnh SELECT * FROM gold_price; và INSERT INTO gold_price(price) VALUES (125.5);.
  
<img width="506" height="154" alt="10" src="https://github.com/user-attachments/assets/69919d0e-b08b-4951-adcc-8aac5a92914f" />

- Xác nhận kết quả lưu trữ: Thực hiện câu lệnh truy vấn dữ liệu để xác nhận thông số kiểm thử kèm mốc thời gian thực của hệ thống đã được ghi nhận thành công vào bảng, dùng lệnh SELECT * FROM gold_price;.

<img width="495" height="152" alt="11" src="https://github.com/user-attachments/assets/9a7dc999-34a6-4df7-bd19-1e8522545703" />


## 2.7. Thu thập dữ liệu với Node-RED    
- Khởi tạo không gian làm việc: Truy cập vào giao diện web của dịch vụ Node-RED để bắt đầu thiết kế luồng thu thập dữ liệu tự động, dùng địa chỉ http://192.168.30.136:1880.
  
<img width="1920" height="980" alt="12" src="https://github.com/user-attachments/assets/2b9c4a8e-eba8-4edd-8882-3bfb3a243c5e" />

- Cài đặt thư viện mở rộng: Truy cập trình quản lý Palette trên giao diện Node-RED để tìm và cài đặt các gói node cần thiết cho dự án bao gồm kết nối InfluxDB, Telegram Bot và MySQL, thao tác trực tiếp trên trình duyệt web.

<img width="1920" height="975" alt="13" src="https://github.com/user-attachments/assets/000031c9-caa7-4453-a861-e656adcaac00" />

- Cấu hình kết nối cơ sở dữ liệu: Mở bảng thuộc tính của node MySQL để thiết lập các thông số máy chủ (host: mariadb), cổng kết nối, tài khoản root và tên database golddb nhằm cấp quyền ghi dữ liệu, thao tác trực tiếp trên giao diện web.
  
<img width="1920" height="915" alt="14" src="https://github.com/user-attachments/assets/a59d07a8-19c8-4798-af94-4cd65d6115a3" />

- Hoàn thiện luồng xử lý: Kết nối các node thành dòng công việc tự động cào dữ liệu API mỗi 10 giây, xử lý và rẽ nhánh lưu song song vào MariaDB, InfluxDB kèm theo chức năng gửi cảnh báo Telegram, thao tác trên giao diện web.
  
<img width="1920" height="916" alt="15" src="https://github.com/user-attachments/assets/8069dbba-4d0e-49ea-83d0-46cff0e4e33b" />

## 2.8. Cấu hình cơ sở dữ liệu InfluxDB
- Lấy thông tin Organization ID: Truy cập giao diện quản trị của InfluxDB để kiểm tra và sao chép mã Organization ID phục vụ cho việc thiết lập kết nối lưu trữ dữ liệu từ Node-RED, thao tác trực tiếp trên trình duyệt qua địa chỉ http://192.168.30.136:8086.
  
<img width="1920" height="972" alt="16" src="https://github.com/user-attachments/assets/8409b413-e020-479e-b1fc-4646e80bfbc6" />

- Truy vấn và trực quan hóa dữ liệu: Sử dụng công cụ Data Explorer của InfluxDB để lọc theo trường dữ liệu gold và xác nhận bản ghi giá vàng kiểm thử (125.5) đã được hệ thống lưu trữ thành công dưới dạng biểu đồ, thao tác trực tiếp trên giao diện web.
  
<img width="1920" height="966" alt="17" src="https://github.com/user-attachments/assets/680f301b-8977-4822-96dd-65c40e344ed4" />

## 2.9. Cấu hình trực quan hóa dữ liệu với Grafana

- Truy cập trang quản trị Grafana: Truy cập vào giao diện trang chủ của dịch vụ Grafana để bắt đầu quá trình thiết lập nguồn dữ liệu và xây dựng biểu đồ theo dõi, thao tác trực tiếp trên trình duyệt qua địa chỉ http://192.168.30.136:3000.

<img width="1920" height="974" alt="18" src="https://github.com/user-attachments/assets/2eebf810-4d92-43ee-ae83-116c7324b45a" />

- Kết nối nguồn dữ liệu InfluxDB: Thiết lập cấu hình kết nối InfluxDB làm nguồn dữ liệu đầu vào cho hệ thống Grafana với ngôn ngữ truy vấn Flux, thao tác trực tiếp trên giao diện web bằng cách khai báo địa chỉ máy chủ nội bộ http://influxdb:8086.

<img width="1920" height="970" alt="19" src="https://github.com/user-attachments/assets/53fae787-ad99-49b9-92f4-be40094b20ae" />

- Lấy mã nhúng biểu đồ: Thiết lập bảng điều khiển (panel) trực quan hóa biến động giá vàng, sau đó mở menu tùy chọn của biểu đồ và chọn "Share embed" để lấy đoạn mã tích hợp trực tiếp vào giao diện web Front-end, thao tác trên giao diện web Grafana.

<img width="1920" height="968" alt="20" src="https://github.com/user-attachments/assets/619d8c63-330e-4348-b3ae-a39f1f33f189" />

- Sao chép mã nhúng biểu đồ: Trích xuất đoạn mã HTML chứa cấu trúc thẻ <iframe> do Grafana tự động sinh ra để mang về dán vào tệp index.html của giao diện Front-end, thao tác bằng cách nhấn nút "Copy to clipboard" trên giao diện web.
  
<img width="914" height="516" alt="21" src="https://github.com/user-attachments/assets/20de401c-9642-40d0-a5fb-ecf2fce9dca0" />

## 2.10. Hoàn thiện giao diện Front-end

- Nhúng biểu đồ vào trang chủ: Mở lại tệp HTML và dán trực tiếp đoạn mã <iframe> vừa lấy từ Grafana vào để tích hợp biểu đồ theo dõi giá vàng lên trang Dashboard, dùng lệnh nano nginx/html/index.html.
  
<img width="1782" height="102" alt="22" src="https://github.com/user-attachments/assets/9e75c64b-09a3-4568-b0c5-9e4d761a0c5f" />

- Kết quả vận hành hệ thống: Truy cập giao diện web để nghiệm thu thành quả cuối cùng, xác nhận trang Dashboard đã hiển thị thành công thông số giá vàng thời gian thực kết hợp biểu đồ lịch sử trực quan, thao tác trên trình duyệt qua địa chỉ IP máy chủ http://192.168.30.136.
  
<img width="1920" height="964" alt="23" src="https://github.com/user-attachments/assets/e7dca247-903d-46a8-93e8-ab32121bb22c" />

## 2.11. Cấu hình cảnh báo qua Telegram

- Khởi tạo Telegram Bot: Truy cập ứng dụng Telegram và nhắn tin với BotFather để tạo bot mới (huagiavang_bot), sau đó sao chép chuỗi mã HTTP API Token phục vụ cho việc thiết lập cấu hình gửi cảnh báo tự động từ Node-RED, thao tác trực tiếp trên ứng dụng Telegram.

<img width="671" height="415" alt="24" src="https://github.com/user-attachments/assets/bcea8412-1f90-4f73-be8d-b6400540bce3" />

- Kiểm tra luồng tin nhắn tự động: Mở ứng dụng Telegram để kiểm tra và xác nhận bot đã nhận được thành công các tin nhắn cảnh báo tự động về biến động giá vàng theo thời gian thực từ hệ thống Node-RED gửi về.
  
<img width="344" height="295" alt="25" src="https://github.com/user-attachments/assets/15196137-78d0-4245-823d-450ddb20d889" />

## 2.12. Mô phỏng sự cố hệ thống

- Kiểm tra lỗi mất kết nối: Truy cập Dashboard sau khi chủ động ngắt các container. Ghi nhận hệ thống báo lỗi "undefined" và mất kết nối biểu đồ Grafana, thao tác trên trình duyệt web.

<img width="1920" height="974" alt="26" src="https://github.com/user-attachments/assets/0ffd8d49-0727-4d48-8dce-5739f9e2b7a1" />

## 2.13. Phục hồi hệ thống

- Tải lại bản sao lưu: Tiến hành nạp lại toàn bộ các ảnh (image) của Docker từ tệp sao lưu dự phòng gold_backup.tar để chuẩn bị khởi động lại các dịch vụ, dùng lệnh sudo docker load -i gold_backup.tar.

<img width="813" height="181" alt="27" src="https://github.com/user-attachments/assets/a7fb51db-3e09-40be-9c88-6fa75d4aca37" />

- Kiểm tra trạng thái sau phục hồi: Liệt kê lại danh sách container để đảm bảo toàn bộ các dịch vụ đã được khôi phục thành công và đang quay trở lại trạng thái hoạt động ổn định (Up), dùng lệnh sudo docker ps.
  
<img width="1534" height="172" alt="28" src="https://github.com/user-attachments/assets/2ac8111e-c780-4773-976b-ae9191088458" />
















