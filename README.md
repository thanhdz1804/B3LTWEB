# B3LTWEB
# Bài tập 3   : môn Phát triển ứng dụng trên nền web
Giảng viên  : Đỗ Duy Cốp
Lớp học phần: 58KTPM
Ngày giao   : 2025-10-24 13:50
Hạn nộp     : 2025-11-05 00:00
## Yêu cầu     : LẬP TRÌNH ỨNG DỤNG WEB trên nền linux
 ## 1. Cài đặt môi trường linux: SV chọn 1 trong các phương án
 - enable wsl: cài đặt docker desktop
 - enable wsl: cài đặt ubuntu
 - sử dụng Hyper-V: cài đặt ubuntu
 - sử dụng VMware : cài đặt ubuntu
 - sử dụng Virtual Box: cài đặt ubuntu
## 2. Cài đặt Docker (nếu dùng docker desktop trên windows thì nó có ngay)
## 3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container sau: 
   mariadb (3306), phpmyadmin (8080), nodered/node-red (1880), influxdb (8086), grafana/grafana (3000), nginx (80,443)
## 4. Lập trình web frontend+backend:
 SV chọn 1 trong các web sau:
### 4.1 Web thương mại điện tử
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.
 - Có tính năng liệt kê các sản phẩm bán chạy ra trang chủ
 - Có tính năng liệt kê các nhóm sản phẩm
 - Có tính năng liệt kê sản phẩm theo nhóm
 - Có tính năng tìm kiếm sản phẩm
 - Có tính năng chọn sản phẩm (đưa sản phẩm vào giỏ hàng, thay đổi số lượng sản phẩm trong giỏ, cập nhật tổng tiền)
 - Có tính năng đặt hàng, nhập thông tin giao hàng => được 1 đơn hàng.
 - Có tính năng dành cho admin: Thống kê xem có bao nhiêu đơn hàng, call để xác nhận và cập nhật thông tin đơn hàng. chuyển cho bộ phận đóng gói, gửi bưu điện, cập nhật mã COD, tình trạng giao hàng, huỷ hàng,...
 - Có tính năng dành cho admin: biểu đồ thống kê số lượng mặt hàng bán được trong từng ngày. (sử dụng grafana)
 - backend: sử dụng nodered xử lý request gửi lên từ javascript, phản hồi về json.
### 4.2 Web IOT: Giám sát dữ liệu IOT.
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.
 - hiển thị giá trị mới nhất của các thông số đang giám sát, khi click vào thì hiển thị đồ thị lịch sử quá trình thay đổi (gọi grafana iframe để hiển thị)
 - backend: Sử dụng nodered để đọc dữ liệu từ các cảm biến (có thể dùng api online để lấy dữ liệu theo giời gian thực), 
   nodered sẽ lưu dữ liệu mới nhất (dạng update) vào cơ sở dữ liệu mariadb (sử dụng phpmyadmin để tạp table và quản trị lần đầu)
   nodered sẽ lưu dữ liệu (insert) vào influxdb để lưu giá trị lịch sử, để cho grafana dùng để hiển thị biểu đồ.
### 5. Nginx làm web-server
 - Cấu hình nginx để chạy được website qua url http://fullname.com  (thay fullname bằng chuỗi ko dấu viết liền tên của bạn)
 - Cấu hình nginx để http://fullname.com/nodered truy cập vào nodered qua cổng 80, (dù nodered đang chạy ở port 1880)
 - Cấu hình nginx để http://fullname.com/grafana truy cập vào grafana qua cổng 80, (dù grafana đang chạy ở port 3000)
Yêu cầu sinh viên lưu code trên github
có file readme.md có hình ảnh + text: ghi lại nhật ký quá trình làm bài.
### CÁCH ĐÁNH GIÁ:
1. Cài đặt được môi trường: 1đ
2. Cài đặt được các docker container với cấu hình phù hợp: 1đ
3. Web chạy được, giao diện phù hợp, chạy trên web sever nginx: 2đ
4. nodered api trả về json, test được: 2đ
5. front-end có js gọi được api nodered, nhận về json, hiển thị được kết quả từ json này. 2đ
6. Bài làm có dấu ấn, giải thích rõ ràng, hiểu vấn đề: 2đ
# BÀI LÀM
## Cài đặt môi trường linux: SV chọn 1 trong các phương án
 - enable wsl: cài đặt docker desktop
 - enable wsl: cài đặt ubuntu
<img width="856" height="571" alt="image" src="https://github.com/user-attachments/assets/7bd65b64-3d97-430a-a506-28b609935abc" />
## 2. Cài đặt Docker (nếu dùng docker desktop trên windows thì nó có ngay)
<img width="1101" height="640" alt="image" src="https://github.com/user-attachments/assets/c6ec8bc9-5267-46e6-a480-c74e51d30ef3" />
## 3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container sau: 
mariadb (3306), phpmyadmin (8080), nodered/node-red (1880), influxdb (8086), grafana/grafana (3000), nginx (80,443)
<img width="771" height="927" alt="image" src="https://github.com/user-attachments/assets/c95a560d-4dd1-4cdc-a3cd-5fc399abb377" />
<img width="1902" height="184" alt="image" src="https://github.com/user-attachments/assets/fe10b54c-0bd8-42ab-8814-a62f26add522" />
## 4. Lập trình web frontend+backend:
## 4.1 Web thương mại điện tử
Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.
<img width="1907" height="927" alt="image" src="https://github.com/user-attachments/assets/06e33aaf-abdb-4a1b-8b5e-d76e8e3e41cc" />

<img width="1450" height="879" alt="image" src="https://github.com/user-attachments/assets/cd388944-3569-4aad-b947-9262842ef3e3" />
<img width="1276" height="678" alt="image" src="https://github.com/user-attachments/assets/1ee2d8ca-53da-4d02-a45f-b3041481d594" />
Thông tin login lưu trong MariaDB, dev quản lý bằng phpMyAdmin, dùng mã hóa khi gửi login
<img width="979" height="242" alt="image" src="https://github.com/user-attachments/assets/427bb749-797c-4c51-aa92-65905e2b825f" />
<img width="1911" height="915" alt="image" src="https://github.com/user-attachments/assets/0eb12070-cc8e-4a6f-a23e-db36a39addc3" />
- Có tính năng liệt kê các sản phẩm bán chạy ra trang chủ
## API “sản phẩm bán chạy”
<img width="1273" height="588" alt="image" src="https://github.com/user-attachments/assets/076bd5dd-6b47-4fb5-9edd-fd99395a7ee3" />
<img width="1553" height="790" alt="image" src="https://github.com/user-attachments/assets/a2cbdb52-a881-42cb-b001-97f431fbcafb" />
<img width="1920" height="919" alt="image" src="https://github.com/user-attachments/assets/98d899a6-3afc-42a7-8824-f4dfa4c10722" />
## - Có tính năng liệt kê các nhóm sản phẩm
<img width="1920" height="985" alt="image" src="https://github.com/user-attachments/assets/e9a19f35-528f-4241-ba2b-633d560efcd8" />
<img width="1226" height="535" alt="image" src="https://github.com/user-attachments/assets/acfb23a1-473b-4f63-b8c0-fb2f1ff53ac4" />
<img width="1907" height="998" alt="image" src="https://github.com/user-attachments/assets/8866d046-16d8-47f8-83ca-3330b22a6ff7" />
## - Có tính năng liệt kê sản phẩm theo nhóm
<img width="1920" height="347" alt="image" src="https://github.com/user-attachments/assets/ed3ca453-925c-4de7-8c21-6915ce25124f" />
<img width="1149" height="449" alt="image" src="https://github.com/user-attachments/assets/57219e4c-c2ec-4747-8a8b-520479fdc2b5" />
<img width="1920" height="938" alt="image" src="https://github.com/user-attachments/assets/e342b1c8-630d-4193-b440-617deeaaf6b6" />
## - Có tính năng tìm kiếm sản phẩm
<img width="1920" height="835" alt="image" src="https://github.com/user-attachments/assets/b76bde15-6014-4c21-a09d-4eda99f0263f" />
<img width="1914" height="928" alt="image" src="https://github.com/user-attachments/assets/f72f72cb-c3e1-4c3f-8501-0be4a33ca32c" />
<img width="1919" height="907" alt="image" src="https://github.com/user-attachments/assets/24910f2f-b260-48c2-8382-74c5760863e1" />
## Chọn sản phẩm (giỏ hàng, tổng tiền)
<img width="1920" height="869" alt="image" src="https://github.com/user-attachments/assets/488be037-a9a3-4e8b-bfd2-000c96b4ce3f" />
<img width="1901" height="794" alt="image" src="https://github.com/user-attachments/assets/6afd80e5-9645-432d-9b87-83971c0a5e66" />
<img width="1385" height="563" alt="image" src="https://github.com/user-attachments/assets/07f01330-e9e3-4be5-a835-0558b6c6c56a" />
## Có tính năng đặt hàng, nhập thông tin giao hàng => được 1 đơn hàng
<img width="1633" height="869" alt="image" src="https://github.com/user-attachments/assets/ee02a8cf-4e59-488e-ad3e-64837247da91" />
<img width="1876" height="761" alt="image" src="https://github.com/user-attachments/assets/b04d20ee-8f2b-4452-b34b-3e1a3bdeba90" />
<img width="1320" height="888" alt="image" src="https://github.com/user-attachments/assets/198a9f2e-140c-41c4-b80c-9334ef3a7877" />
## Có tính năng dành cho admin: Thống kê xem có bao nhiêu đơn hàng, call để xác nhận và cập nhật thông tin đơn hàng. chuyển cho bộ phận đóng gói, gửi bưu điện, cập nhật mã COD, tình trạng giao hàng, huỷ hàng,...
<img width="1159" height="700" alt="image" src="https://github.com/user-attachments/assets/f1217926-afe1-457e-9020-6972de328a87" />
<img width="1272" height="504" alt="image" src="https://github.com/user-attachments/assets/4ad9b909-05c8-4311-b975-2577d65b8cc5" />
<img width="1661" height="934" alt="image" src="https://github.com/user-attachments/assets/0333e88d-1317-41f0-b610-fe6c5789c32c" />
<img width="1913" height="979" alt="image" src="https://github.com/user-attachments/assets/f3c6956f-2ea5-47db-b704-7e6f454c8f31" />
<img width="1181" height="964" alt="image" src="https://github.com/user-attachments/assets/4ef40f22-8bb4-40af-a26b-88897e3eca06" />
<img width="1716" height="922" alt="image" src="https://github.com/user-attachments/assets/a63863fb-b37f-48d8-965f-2fc03232111d" />
## - Có tính năng dành cho admin: biểu đồ thống kê số lượng mặt hàng bán được trong từng ngày. (sử dụng grafana)
<img width="1274" height="715" alt="image" src="https://github.com/user-attachments/assets/5e7f0924-1be7-431e-b340-c7bfafa2db43" />
<img width="1920" height="633" alt="image" src="https://github.com/user-attachments/assets/a0844c0b-9bbc-4323-b605-c344b1038d01" />
<img width="1917" height="902" alt="image" src="https://github.com/user-attachments/assets/35b3ecfd-374e-4ed8-9313-b350f93ff281" />
##  - backend: sử dụng nodered xử lý request gửi lên từ javascript, phản hồi về json.
<img width="1672" height="916" alt="image" src="https://github.com/user-attachments/assets/a2bff607-c92e-4a65-a2c0-c21a0d5f86f5" />
<img width="1178" height="456" alt="image" src="https://github.com/user-attachments/assets/f727f0df-21ea-4b7d-8d5b-602b7ca32d75" />
# 5. Nginx làm web-server
 - Cấu hình nginx để chạy được website qua url http://fullname.com  (thay fullname bằng chuỗi ko dấu viết liền tên của bạn)
 - Cấu hình nginx để http://fullname.com/nodered truy cập vào nodered qua cổng 80, (dù nodered đang chạy ở port 1880)
 - Cấu hình nginx để http://fullname.com/grafana truy cập vào grafana qua cổng 80, (dù grafana đang chạy ở port 3000)






