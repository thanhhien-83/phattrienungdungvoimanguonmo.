## PHÁT TRIỂN ỨNG DỤNG CỘNG MÃ NGUỒN MỞ (DJANGO + XÂY DỰNG WEBSITE QUẢN LÝ TIỆM CẦM ĐỒ)
### TÊN: HỨA THỊ THANH HIỀN
### LỚP: K58KTP
### MSSV: K225480106016
### Deadline: 23h59 - 09/05/2026

## <p align="center">BÀI LÀM</p>

### 1. Chuẩn bị Ubuntu
- Kiểm tra phiên bản Docker: `docker --version`

- Kiểm tra phiên bản Docker Compose: `docker compose version`

<img width="1082" height="240" alt="1" src="https://github.com/user-attachments/assets/aa811dac-e8ba-4ca5-b8bc-b4d6bf1ba6a1" />

***Hình 1: Kiểm tra phiên bản Docker và Docker Compoes***

### 2. Tạo thư mục Project

- Tạo thư mục `mkdir camdo_project`

- Trỏ vào thư mục `cd camdo_project`

<img width="1240" height="747" alt="2" src="https://github.com/user-attachments/assets/2accae42-da00-4ccb-8c82-5b017a3e938f" />

***Hình 2: Tạo thư mục dự án camdo_project***

<img width="1105" height="757" alt="3" src="https://github.com/user-attachments/assets/e7dd90cd-fb01-4b7e-85f2-d00ab5096ea4" />

***Hình 3: Tạo thư mục django và kiểm tra danh sách thư mục cấu trúc dự án bằng lệnh `ls`***

### 3. Tạo file Dockerfile

- Trỏ vào thư mục Django: `cd django`

- Tạo file DockerFile: `nano Dockerfile`

- Thêm nội dung cấu hình cho File: ***dockerfile***. Và sử dụng `Ctrl + O` -> `Enter` -> `Ctrl + X` để tiến hành lưu file ***dockerfile***.

***Các thành phần chính của Dockerfile. Một Dockerfile tiêu chuẩn thường bao gồm các lệnh sau:***

```
- FROM: Khai báo hệ điều hành nền hoặc môi trường ngôn ngữ (Ví dụ: python:3.10-slim).

- WORKDIR: Thiết lập thư mục làm việc chính bên trong container.

- COPY: Sao chép mã nguồn từ máy tính cá nhân vào trong image.

- RUN: Thực thi các câu lệnh cài đặt (Ví dụ: pip install -r requirements.txt).

- ENV: Thiết lập các biến môi trường (như giúp Python không tạo ra các file .pyc thừa).

- CMD: Câu lệnh mặc định để khởi chạy ứng dụng khi container bắt đầu chạy.
```
<img width="1478" height="758" alt="4" src="https://github.com/user-attachments/assets/79a14e24-15cd-4e59-8c32-bc373f7f4c0d" />

***Hình 4: Cấu hình nội dung và tạo file dockerfile***

### 4. Tạo file requirements.txt

- Tạo file ***requirements.txt*** lệnh: `nano requirements.txt`. Và sử dụng `Ctrl + O` -> `Enter` -> `Ctrl + X` để tiến hành lưu file ***requirements.txt***.

***Các thành phần chính trong dự án. Dựa trên dự án quản lý tiệm cầm đồ hiện tại, file requirements.txt của bạn bao gồm:***

```
- django: Khung sườn (framework) chính để xây dựng website.

- pandas & numpy: Dùng để xử lý dữ liệu, tính toán số liệu quá hạn và hỗ trợ vẽ biểu đồ.

- django-chartjs (hoặc các thư viện tương đương): Hỗ trợ kết nối dữ liệu từ Python sang biểu đồ Chart.js trên giao diện.

- gunicorn: Server giúp chạy Django một cách ổn định khi bạn public ra internet.
```

<img width="1478" height="756" alt="5" src="https://github.com/user-attachments/assets/99304f56-8a9b-4b30-8473-0fb3b1add25e" />

***Hình 5: Cấu hình tạo file requirements.txt***

### 5. Tạo file docker-compose.yml

- Quay lại thư mục gốc: `cd ..`

- Tạo file ***docker-compose.yml*** lệnh: `nano docker-compose.yml`. Và sử dụng `Ctrl + O` -> `Enter` -> `Ctrl + X` để tiến hành lưu file ***docker-compose.yml***.

- Sau khi hoàn thiện file ***docker-compose.yml*** tiến hành build Container lệnh: `docker compose up -d --build`

- Kiểm tra container hoạt động bằng lệnh: `docker ps`

***Cấu trúc cơ bản trong dự án. Dựa trên cấu trúc dự án camdo_project, file này thường điều phối các dịch vụ sau:***

```
- version: Xác định phiên bản của Docker Compose đang sử dụng.

- services: Danh sách các container cấu thành ứng dụng:

- django: Container chạy mã nguồn ứng dụng Django, thực hiện logic nghiệp vụ và hiển thị Dashboard.

- db: Container chạy hệ quản trị cơ sở dữ liệu (thường là PostgreSQL hoặc MySQL) để lưu trữ thông tin hợp đồng và khách hàng.

- volumes: Cơ chế chia sẻ dữ liệu giữa máy vật lý (WSL2) và container, giúp code thay đổi trong VS Code được cập nhật ngay lập tức vào container mà không cần build lại.

- ports: Ánh xạ cổng từ máy vật lý vào container (Ví dụ: 8000:8000), có thể truy cập web qua localhost:8000.
```

<img width="1477" height="746" alt="6" src="https://github.com/user-attachments/assets/ae3039d8-6f98-45e1-a5b5-373fe5632148" />

***Hình 6: Cấu hình nội dung tạo file docker-compose.yml***

👉 Kết quả phải thấy 3 service: **mariadb + phpmyadmin + django_app** đang hoạt động ở trạng thái UP.

### 6. Tạo file setting.py

***Các thành phần then chốt***
```
- DEBUG: Thiết lập chế độ gỡ lỗi. Trong quá trình phát triển dự án, Thứ thường để True, nhưng khi public ra Internet qua Cloudflare, cần lưu ý về bảo mật.

- ALLOWED_HOSTS: Danh sách các tên miền hoặc địa chỉ IP được phép truy cập vào website. Thứ đã cấu hình tên miền chính nguyenthu.id.vn tại đây để hệ thống chấp nhận yêu cầu từ Tunnel.

- INSTALLED_APPS: Danh sách các ứng dụng (modules) được kích hoạt trong dự án, ví dụ như management (ứng dụng quản lý tiệm cầm đồ) hay các thư viện hỗ trợ vẽ biểu đồ.

- DATABASES: Cấu hình kết nối với cơ sở dữ liệu (Database). Đây là nơi Thứ thiết lập để Django biết cách lưu trữ thông tin hợp đồng và khách hàng vào container DB.

- TEMPLATES: Quy định nơi chứa các file HTML (như file home.html có biểu đồ mà Thứ vừa nâng cấp) để hiển thị giao diện cho người dùng.
```

<img width="1486" height="755" alt="7" src="https://github.com/user-attachments/assets/d41aa203-ef45-4a9c-9e18-9e4519099a4e" />

***Hình 7: Cấu hình tạo file setting.py***

### 7. Tạo file models.py

***Các thực thể chính trong dự án. Dựa trên dự án quản lý tiệm cầm đồ, file này thường định nghĩa các bảng sau:***

```
- Customer: Lưu trữ thông tin cá nhân của khách nợ như Họ tên, Số điện thoại (SĐT), và Số CCCD.

- PawnItem: Định nghĩa thông tin về tài sản cầm cố (Tên tài sản, Loại tài sản).

- Contract (Hợp đồng): Đây là bảng quan trọng nhất, kết nối Khách hàng và Tài sản, đồng thời lưu trữ các thông tin nghiệp vụ như:

    Số tiền vay gốc.

    Lãi suất.

    Ngày bắt đầu và ngày đến hạn.
```

<img width="1492" height="773" alt="8" src="https://github.com/user-attachments/assets/960e6acf-e9e8-46b3-96ac-376932fb32f4" />

***Hình 8: Cấu hình tạo file models.py***

### 8. Tạo file admin.py

***Chức năng chính trong dự án. Trong hệ thống quản lý tiệm cầm đồ, file này thực hiện các nhiệm vụ:***

```
Đăng ký Models: Kết nối các bảng dữ liệu từ models.py (như Khách hàng, Hợp đồng) vào trang quản trị.

Tùy biến hiển thị: Quy định những thông tin nào sẽ hiện ra trong danh sách quản lý, ví dụ: hiển thị cột Tên khách hàng, Số điện thoại và Trạng thái nợ thay vì chỉ hiện tên chung chung.

Bộ lọc và Tìm kiếm: Thiết lập các thanh tìm kiếm (theo tên khách hàng) và bộ lọc (theo ngày quá hạn) để quản lý hàng nghìn hợp đồng một cách nhanh chóng.
```

<img width="1496" height="761" alt="9" src="https://github.com/user-attachments/assets/d69ff1d9-abd2-49f1-992f-84eb716ebe1a" />

***Hình 9: Cấu hình tạo file admin.py***

### 9. Truy cập Django

- Truy cập ***Django*** với địa chỉ link localhost: http://localhost:8000/admin/shopapp/customer/

<img width="1918" height="637" alt="10" src="https://github.com/user-attachments/assets/be20c193-97fd-4da2-a7c9-975acf723f38" />

***Hình 10: Giao diện trang quản trị Django với các tính năng như: Thêm khách hàng, mặt hàng, khoản vay****

### 10. Truy cập phpMyAdmin

- Truy cập ***phpMyAdmin*** với đại chỉ link localhost: http://localhost:8080

<img width="1918" height="961" alt="11" src="https://github.com/user-attachments/assets/05019f73-3fd6-41a9-952a-5c528493199b" />

***Hình 11: Giao diện trang chủ phpMyAdmin với các bảng dữ liệu trong Database***

### 11. Cập nhật lại file models.py

- Tiến hành cập nhật file ***models.py***. Và sử dụng `Ctrl + O` -> `Enter` -> `Ctrl + X` để tiến hành lưu file ***models.py***.

<img width="1472" height="756" alt="12" src="https://github.com/user-attachments/assets/47cd927a-449b-4316-8317-63ab02674c22" />

***Hình 12: Cập nhật file models.py***

### 12. Tạo file home.html

- Tạo file ***home.html*** thông qua lệnh nano để tạo ra giao diện trang chủ.

<img width="1473" height="753" alt="13" src="https://github.com/user-attachments/assets/7a1798d1-e846-47e9-ae92-4e2a73a0d5f2" />

***Hình 13: Cấu hình nội dung file home.html***

### 13. Tạo file view.py

<img width="1401" height="545" alt="14" src="https://github.com/user-attachments/assets/bcc217c8-0adc-4d47-bf16-b1c1f0274c31" />

***Hình 14: Cấu hình nội dung file view.py***

### 14. Tạo file urls.py

<img width="1475" height="312" alt="15" src="https://github.com/user-attachments/assets/12085cc7-e127-45b2-9a33-487b82ffad6d" />

***Hình 15: Cấu hình nội dung file view.py***

### 15. Truy cập trang chủ website cầm đồ

- Truy cập thông qua địa chỉ localhost link: http://127.0.0.1:8000

<img width="1917" height="377" alt="16" src="https://github.com/user-attachments/assets/4e8f90e2-f693-42ff-a655-f0494e3406a2" />

***Hình 16: Giao diện trang chủ website cầm đồ với các thông tin và thuộc tính khách***

### 16. Public Django lên Subdomain bằng Cloudfare Tunner

- Dowload ***claudfare tunnel*** vào Ubuntu bằng lệnh: `wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb`

<img width="1463" height="732" alt="17" src="https://github.com/user-attachments/assets/464bba59-3ee3-4fde-b16e-38132bf3dd99" />

***Hình 17: Quá trình cài đặt đang diễn ra***

- Cài đặt: `sudo dpkg -i cloudflared-linux-amd64.deb`

- Kiểm tra version Cloudfare: `cloudflared --version`

<img width="1151" height="215" alt="18" src="https://github.com/user-attachments/assets/518e9180-2739-4f19-a44c-d5101bd39c2b" />

***Hình 18: Qua trình cài đặt và kiểm tra version đang diễn ra***

### LOGIN CLOUDFLARE

- Chạy lệnh: 'cloudflared tunnel login` sẽ sinh ra 1 địa chỉ để login vào claudfare tunnel.

- Truy cập địa chỉ đó trên trình duyệt để tiéng hành đăng nhập Cloudfare.

- Chọn đúng domain -> Chọn Authorize.

<img width="1918" height="1017" alt="19" src="https://github.com/user-attachments/assets/1e1d184c-6948-4f45-bf16-9f60e4ac9278" />

***Hình 19: Sau khi click sẽ hiện thông báo đồng thời trên ubuntu cũng thông báo You have successfully logged in và sinh ra file .pem thành công***

### TẠO TUNNEL

- Chạy lệnh: `cloudflared tunnel create camdo-tunnel` sẽ sinh ra 1 dãy id và tiếng hành coppy lại.

- Tạo file ***config.yml*** bằng lệnh: `nano ~/.cloudflared/config.yml`

- Thêm nội dung sau ( Vì dùng chung đường hầm với web cũ nên không cần thêm id, có thể dùng chung ip với web cũ) và dán mã id vừa coppy vào trong file config.py.

<img width="1467" height="445" alt="20" src="https://github.com/user-attachments/assets/3e36e444-7217-41b4-829d-725838c6cc10" />

***Hình 20: Cấu hình nội dung file config.yml***

### CHẠY TUNNEL

- Chạy lệnh `cloudflared tunnel run camdo-tunnel`

<img width="1460" height="740" alt="21" src="https://github.com/user-attachments/assets/1343725a-2736-4dca-b62d-ef4404b72972" />

***Hình 21: Qua trình chạy Tunner đang diễn ra***

- Giao diện Website chạy thành công với link Cloudfare: http://camdo.huathanhhien.id.vn hiển thị danh sách giao dịch cần đồ quá hạn.
  
<img width="1918" height="967" alt="22" src="https://github.com/user-attachments/assets/6b3d5e6d-224d-4c2d-a2d7-bc7b866c6839" />

***Hình 22: Giao diện Web cầm đồ thành công chạy qua Cloudfare***

### 19. Đánh giá nhận xét

***1. Tính thực tiễn và ứng dụng (Practicality)***

- Đề tài "Hệ thống quản lý tiệm cầm đồ thông minh" không dừng lại ở mức bài tập kỹ năng mà đã giải quyết trực tiếp các vấn đề nhức nhối của mô hình kinh doanh cầm đồ truyền thống:

- Tự động hóa tính toán: Loại bỏ sai sót con người trong việc tính lãi suất, ngày quá hạn và tổng nợ.

- Trực quan hóa dữ liệu: Sử dụng Dashboard với biểu đồ sinh động (Chart.js) giúp chủ cửa hàng nắm bắt tình hình kinh doanh chỉ trong vài giây.

***2. Sự kết hợp công nghệ (Tech Stack Evaluation)***

- Dự án thể hiện sự am hiểu sâu sắc về các công nghệ lập trình và hạ tầng hiện đại:

- Backend vững chắc: Sử dụng Django Framework giúp quản lý logic nghiệp vụ phức tạp và bảo mật dữ liệu cao qua file settings.py và models.py.

- Kiến trúc Containerization: Việc triển khai toàn bộ ứng dụng trên Docker & Docker Compose giúp hệ thống có tính đóng gói cao, dễ dàng di chuyển và triển khai trên mọi môi trường mà không lo xung đột thư viện.

- Giải pháp triển khai đột phá: Sử dụng Cloudflare Tunnel để biến máy tính cá nhân thành một máy chủ Public qua tên miền riêng (nguyenthu.id.vn) là một bước đi thông minh, tiết kiệm chi phí thuê VPS nhưng vẫn đảm bảo bảo mật qua lớp Proxy của Cloudflare.

***3. Khả năng mở rộng (Scalability)***

- Cấu trúc mã nguồn được phân tách rõ ràng theo mô hình MVC (Model-View-Controller):

- Dễ dàng nâng cấp thêm các tính năng như: Quản lý kho thanh lý, Gửi thông báo nhắc nợ tự động qua SMS/Zalo, hoặc tích hợp thanh toán trực tuyến.

- Cơ sở dữ liệu được định nghĩa chuẩn xác trong models.py, sẵn sàng cho việc xử lý hàng vạn hợp đồng cùng lúc.

***4. Kết luận***

- Đây là một dự án hoàn thiện, thể hiện tư duy Full-stack từ việc thiết kế Database, xử lý Logic Backend, xây dựng Frontend trực quan cho đến việc cấu hình hạ tầng mạng và tên miền chuyên nghiệp.

- Đề tài này là minh chứng rõ nét cho khả năng làm chủ công nghệ và giải quyết bài toán thực tế của người thực hiện.

## <p align="center">KẾT THÚC</p>












































