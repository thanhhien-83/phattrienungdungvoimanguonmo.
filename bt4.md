## Môn: Phát triển ứng dụng với mã nguồn mở-TEE0421
## Hứa Thị Thanh Hiền
## Lớp: 58KTPM
# Bài tập 04:

## KHAI THÁC N8N ĐỂ TỰ ĐỘNG ĐĂNG BÀI LÊN WORDPRESS
deadline : 23h59 ngày 25 tháng 5 năm 2026.
SỬ DỤNG KẾT QUẢ ĐÃ LÀM Ở BÀI TẬP 3, BỔ SUNG VÀO DOCKER COMPOSE ĐỂ CÓ THÊM SERVICE 8N8:
1. Cấu hình các file trong dokcer-compose.yml:  

- Mariadb:  
<img width="405" height="360" alt="Screenshot 2026-05-25 153451" src="https://github.com/user-attachments/assets/8b546a95-5ec2-4642-baa4-b663ca8bc6df" />  

- PhPAdmin:  
<img width="393" height="282" alt="2" src="https://github.com/user-attachments/assets/32e485d2-0b97-4151-8897-f57d9f0ce365" />  

- WordPress:  
<img width="617" height="357" alt="3" src="https://github.com/user-attachments/assets/0d7980cd-2c9f-4a3b-a687-70a8e245b6a2" />   

- Cấu hình Tunel cloudflare để truy cập vào các dịch vụ bằng các subdomain ( em sử dụng lệnh cli thay cho việc thao tác đồ họa trên dashboard của cloudflare):  

- Tạo tunel của 3 sub-domain:  
<img width="1102" height="201" alt="4" src="https://github.com/user-attachments/assets/8d5e8c14-8e5f-4074-bb63-e035aa3999bc" />  

- Thêm chuỗi id tunel vào config.yml:  
<img width="806" height="396" alt="5" src="https://github.com/user-attachments/assets/7ca9f957-46ef-4aa4-beb8-ec1fa87ce276" />  

- Cấu hình dịch vụ cloudflare trong docker-compose.yml:  
<img width="669" height="321" alt="image" src="https://github.com/user-attachments/assets/b9d3f1da-d373-4035-9703-d8b2c6c814e3" />  


- n8n:
<img width="476" height="323" alt="7" src="https://github.com/user-attachments/assets/31fc4726-3d17-4b73-8d8d-0320d741032b" />  


- Pull các images về và chạy chúng:  
<img width="533" height="217" alt="9" src="https://github.com/user-attachments/assets/f90d31e4-7191-44b4-903a-fc5466571cca" />  

2. Kiểm tra truy cập các sub-domain:   
- Truy cập sub-domain2 để quan sát xem cơ sở dữ liệu chưa có bảng nào:  
<img width="1918" height="615" alt="8" src="https://github.com/user-attachments/assets/188c53de-4696-429d-983a-2196622c566d" />  

- Truy cập sub-domain1 để cài đặt wordpress:  
<img width="1918" height="718" alt="10" src="https://github.com/user-attachments/assets/4ddf9938-3408-4110-847e-0741fa5ca063" />  

- Truy cập sub-domain2 để quan sát xem cơ sở dữ liệu có những bảng dữ liệu nào sau khi cài wp:  
<img width="1918" height="968" alt="11" src="https://github.com/user-attachments/assets/df2737ff-31e2-4608-90c8-ce4bb5d2b404" />  

- Tạo 1 bài viết trong wordpress giới thiệu về bản thân sinh viên: thông tin cá nhân, sở thích, ... bài viết có thể chứa hình ảnh, âm thanh, video, ...  
<img width="1918" height="966" alt="12" src="https://github.com/user-attachments/assets/190b4625-2703-4c42-b0cf-7e3d175b0847" />  

- Tạo 1 bài viết trong wordpress giới thiệu về những kiến thức mà em đã học được ở môn Phát triển ứng dụng với mã nguồn mở  
<img width="1918" height="967" alt="13" src="https://github.com/user-attachments/assets/015c0b5b-0440-4ec8-94ba-7d44de8d6f42" />  

- Truy cập sub-domain3 để cấu hình n8n:  
tạo tài khoản admin :  
<img width="1916" height="906" alt="14" src="https://github.com/user-attachments/assets/b6c163ce-ade5-4114-91b1-72ad457be930" />

3. Cấu hình n8n:  
- Send me a Licence key:  
<img width="670" height="752" alt="15" src="https://github.com/user-attachments/assets/f9aa118b-d7cd-4463-ab06-251761ac166f" />  


- Activate License key: ( trang chủ -> setting -> usage and plan -> enter activation key -> điền key vừa nhận từ email vào):  
<img width="693" height="357" alt="16" src="https://github.com/user-attachments/assets/1f715927-9ff5-46cd-a342-2b1de5ab5f8e" />

- Sau khi tạo bot mới cần copy lấy Token  
<img width="1342" height="736" alt="18" src="https://github.com/user-attachments/assets/235a5279-aac0-45be-83af-b9efc1e77752" />

- Add (nối tiếp vào sau node Telegram Trigger) node: AI Google Gemini => Message a model => Set up Credential => cần Nhập API KEY  
<img width="1284" height="2778" alt="image" src="https://github.com/user-attachments/assets/ae44ef42-8d44-4f21-88dc-19e82c28eacd" />
<img width="1284" height="2778" alt="image" src="https://github.com/user-attachments/assets/95125484-b0d8-49ce-91cb-eb27e7c0b3cd" />

<img width="702" height="508" alt="19" src="https://github.com/user-attachments/assets/b13aa020-6632-42f3-8437-406a9aa1bd0e" />

<img width="1327" height="716" alt="20" src="https://github.com/user-attachments/assets/f8521d0f-838c-464c-9711-4030a1c40c99" />

<img width="1628" height="866" alt="21" src="https://github.com/user-attachments/assets/cf755a9e-37cf-4176-ac26-c70c82b28483" />

<img width="611" height="445" alt="22" src="https://github.com/user-attachments/assets/486c9805-c582-4b6a-935f-fe6b43297785" />

<img width="1850" height="852" alt="24" src="https://github.com/user-attachments/assets/39147b98-60a5-4f5a-a15f-3044d75a4fbf" />

<img width="1918" height="1032" alt="25" src="https://github.com/user-attachments/assets/7c5f19da-8ce5-4465-b01c-ff0e028072c2" />

<img width="1343" height="730" alt="26" src="https://github.com/user-attachments/assets/870f47e5-51e4-482b-a4eb-78f5636fde4b" />

<img width="1840" height="842" alt="27" src="https://github.com/user-attachments/assets/19cb0ca2-d3c4-4972-a9b1-6c9443c1ce13" />

<img width="1918" height="1027" alt="28" src="https://github.com/user-attachments/assets/791dc247-fe74-4406-b028-5b72c7dc019a" />

4. Nhận xét kết quả đạt được:  
- Đã triển khai thành công hệ thống gồm MariaDB, PhpMyAdmin, WordPress, Cloudflared và n8n bằng Docker Compose trên Ubuntu. Các service hoạt động ổn định và được public ra Internet thông qua Cloudflare Tunnel.  

- Cấu hình thành công workflow tự động:  
- Telegram Bot → Google Gemini AI → xử lý dữ liệu bằng JavaScript → tự động đăng bài lên WordPress bằng n8n.  

- Qua bài thực hành, em đã hiểu cách sử dụng Docker, Cloudflare Tunnel, WordPress, n8n và tích hợp AI để xây dựng hệ thống tự động hóa thực tế.  
