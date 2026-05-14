# HƯỚNG DẪN SỬ DỤNG KIKO LAND AUTO - FINAL VERSION (WITH LICENSE)

## 1. Yêu Cầu Hệ Thống
- Đã cài đặt Node.js (Phiên bản mới nhất).
- Cài đặt các thư viện cần thiết bằng lệnh sau trong thư mục tool:
  npm install 

## 2. Chi Tiết Các File Cấu Hình (Cần tạo đúng tên file)

### A. Các file bắt buộc phải có dữ liệu:
1. privatekey.txt:
   - Chứa danh sách Private Key ví (mỗi dòng 1 key).
2. proxy.txt:
   - Chứa danh sách Proxy (định dạng http://user:pass@ip:port hoặc http://ip:port). Mỗi dòng 1 proxy.
3. ref.txt:
   - Mã giới thiệu (Ref code) bạn muốn sử dụng để chéo hoặc ủng hộ. Mỗi dòng 1 mã. Tool sẽ lấy xoay vòng theo thứ tự ví.
4. User_agents.txt:
   - Danh sách User Agent trình duyệt. Mỗi dòng 1 chuỗi UA. 
5. Config.json:
   - File cấu hình thông số chạy. Copy nội dung mẫu bên dưới:
   {
     "threads": 1,
     "startInterval": 2,
     "minDelayNextAccount": 30,
     "maxDelayNextAccount": 60,
     "enableRef": true
   }

### B. Các file hệ thống (Tự động sinh ra hoặc dùng để quản lý):
6. license.txt: 
   - Lưu mã Key bản quyền của bạn. Nếu chưa có, tool sẽ yêu cầu nhập lúc khởi động lần đầu.
7. index.txt: 
   - Lưu vị trí ví đang chạy dở. Tool sẽ tự chạy tiếp nếu bị tắt đột ngột.
8. profiles.json: 
   - Lưu session, refresh token và lịch sử điểm danh của từng ví để tránh login lại nhiều lần.
9. uref.txt: 
   - Nơi tool tự động lưu lại mã Ref của chính ví bạn sau khi login thành công (để lấy đi chéo ví khác).

## 3. Các Bước Vận Hành

Bước 1: Chuẩn bị đầy đủ các file .txt và .json như danh sách trên.
Bước 2: Mở Terminal/Command Prompt tại thư mục tool.
Bước 3: Chạy lệnh: node Full.js
Bước 4: Nhập License Key (nếu là lần đầu chạy).
   - Tool sẽ kiểm tra HWID (mã máy) của bạn với Server.
   - Nếu Key đúng, tool sẽ bắt đầu chạy.

## 4. Cơ Chế Hoạt Động Đặc Biệt
- Tự Động Reset: Đúng 7:00 AM (giờ Việt Nam) hàng ngày, tool sẽ tự động đưa `index` về 0 để chạy lại lượt điểm danh mới cho toàn bộ ví.
- Đa Luồng (Threads): Bạn có thể chỉnh số luồng trong Config.json để chạy nhiều ví cùng lúc.
- Kháng Lỗi: Nếu Proxy lỗi hoặc mạng yếu, tool sẽ tự động thử lại sau 3 giây.
- Quản Lý IP: Mỗi ví sẽ được gán một Proxy ngẫu nhiên trong danh sách để đảm bảo an toàn.

## 5. Lưu Ý
- Không xóa file `profiles.json` nếu muốn duy trì streak điểm danh ổn định.
- Nếu muốn chạy lại từ đầu (ví số 1), hãy sửa số trong `index.txt` thành 0.
- License Key gắn liền với mã máy (HWID), không thể dùng chung cho máy khác trừ khi được admin reset.
