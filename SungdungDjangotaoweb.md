## PHÁT TRIỂN ỨNG DỤNG CỘNG MÃ NGUỒN MỞ (DJANGO + XÂY DỰNG WEBSITE QUẢN LÝ TIỆM CẦM ĐỒ)
### TÊN: HỨA THỊ THANH HIỀN
### LỚP: K58KTP
### MSSV: K225480106016

## <p align="center">BÀI LÀM</p>

### 1. Chuẩn bị Ubuntu
- Kiểm tra phiên bản Docker: `docker --version`

- Kiểm tra phiên bản Docker Compose: `docker compose version`

<img width="1082" height="240" alt="1" src="https://github.com/user-attachments/assets/aa811dac-e8ba-4ca5-b8bc-b4d6bf1ba6a1" />

***Hình 1: Kiểm tra phiên bản Docker và Docker Compoes***

- Tạo thư mục `mkdir camdo_project`

- Trỏ vào thư mục `cd camdo_project`

<img width="1240" height="747" alt="2" src="https://github.com/user-attachments/assets/2accae42-da00-4ccb-8c82-5b017a3e938f" />

***Hình 2: Tạo thư mục dự án camdo_project***

<img width="1105" height="757" alt="3" src="https://github.com/user-attachments/assets/e7dd90cd-fb01-4b7e-85f2-d00ab5096ea4" />

***Hình 3: Tạo thư mục django và kiểm tra danh sách thư mục bằng lệnh `ls`***

- Vào thư mục Django: `cd django`

- Tạo file DockerFile: `nano Dockerfile`

- Thêm nội dung cho File: ***dockerfile***. Sử dụng `Ctrl + O` -> Enter -> `Ctrl + X`.

<img width="1478" height="758" alt="4" src="https://github.com/user-attachments/assets/79a14e24-15cd-4e59-8c32-bc373f7f4c0d" />

***Hình 4: Cấu hình tạo file dockerfile***

- Tạo file: ***requirements.txt***

- Tạo file `requirements.txt` lệnh: `nano requirements.txt`

<img width="1478" height="756" alt="5" src="https://github.com/user-attachments/assets/99304f56-8a9b-4b30-8473-0fb3b1add25e" />

***Hình 5: Cấu hình tạo file requirements.txt***

- Tạo file ***DOCKER - COMPOSE.YML***

- Quay lại thư mục gốc: `cd ..`

- Tạo file `docker-compose.yml` lệnh: `nano docker-compose.yml`

- Sau khi hoàn thiện file `docker-compose.yml` tiếng hành biuld Container lệnh: `docker compose up -d --build`

- Kiểm tra container bằng lệnh: `docker ps`

<img width="1477" height="746" alt="6" src="https://github.com/user-attachments/assets/ae3039d8-6f98-45e1-a5b5-373fe5632148" />

***Hình 6: Cấu hình tạo file docker-compose.yml***

<img width="1486" height="755" alt="7" src="https://github.com/user-attachments/assets/d41aa203-ef45-4a9c-9e18-9e4519099a4e" />

***Hình 7: Cấu hình tạo file setting.py***

<img width="1492" height="773" alt="8" src="https://github.com/user-attachments/assets/960e6acf-e9e8-46b3-96ac-376932fb32f4" />

***Hình 8: Cấu hình tạo file models.py***

<img width="1496" height="761" alt="9" src="https://github.com/user-attachments/assets/d69ff1d9-abd2-49f1-992f-84eb716ebe1a" />

***Hình 9: Cấu hình tạo file***

<img width="1918" height="637" alt="10" src="https://github.com/user-attachments/assets/be20c193-97fd-4da2-a7c9-975acf723f38" />

***Hình 10: Cấu****

<img width="1918" height="961" alt="11" src="https://github.com/user-attachments/assets/05019f73-3fd6-41a9-952a-5c528493199b" />

***Hình 11:***

<img width="1472" height="756" alt="12" src="https://github.com/user-attachments/assets/47cd927a-449b-4316-8317-63ab02674c22" />

***Hình 12:***

<img width="1473" height="753" alt="13" src="https://github.com/user-attachments/assets/7a1798d1-e846-47e9-ae92-4e2a73a0d5f2" />

***Hình 13:***

<img width="1401" height="545" alt="14" src="https://github.com/user-attachments/assets/bcc217c8-0adc-4d47-bf16-b1c1f0274c31" />

***Hình 14:***

<img width="1475" height="312" alt="15" src="https://github.com/user-attachments/assets/12085cc7-e127-45b2-9a33-487b82ffad6d" />

***Hình 15:***

<img width="1917" height="377" alt="16" src="https://github.com/user-attachments/assets/4e8f90e2-f693-42ff-a655-f0494e3406a2" />

***Hình 16:***

<img width="1463" height="732" alt="17" src="https://github.com/user-attachments/assets/464bba59-3ee3-4fde-b16e-38132bf3dd99" />

***Hình 17:***

<img width="1151" height="215" alt="18" src="https://github.com/user-attachments/assets/518e9180-2739-4f19-a44c-d5101bd39c2b" />

***Hình 18:***

<img width="1918" height="1017" alt="19" src="https://github.com/user-attachments/assets/1e1d184c-6948-4f45-bf16-9f60e4ac9278" />

***Hình 19:***

-

<img width="1467" height="445" alt="20" src="https://github.com/user-attachments/assets/3e36e444-7217-41b4-829d-725838c6cc10" />

***Hình 20: Cấu hình file config.yml***

<img width="1460" height="740" alt="21" src="https://github.com/user-attachments/assets/1343725a-2736-4dca-b62d-ef4404b72972" />

***Hình 21:***

- Giao diện Website chạy thành công với link: `http://camdo.huathanhhien.id.vn` với danh sách giao dịch cần đồ quá hạn.
  
<img width="1918" height="967" alt="22" src="https://github.com/user-attachments/assets/6b3d5e6d-224d-4c2d-a2d7-bc7b866c6839" />

***Hình 22: Giao diện Web cầm đồ thành công chạy trên Cloudfare***














































