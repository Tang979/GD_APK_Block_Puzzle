# Block Puzzle

## Video Gameplay
[Watch Gameplay](link)

## APK
[Download APK](link)

## Source Code
[View Source Code](https://github.com/nguyenkhacnhat203-dev/BlockPuzzle)

---

## 1. Tổng quan
- **Tên game:** Block Puzzle  
- **Thể loại:** Puzzle  
- **Nền tảng:** Mobile (Android / iOS)  
- **Chế độ chơi:** Single-player  
- **Đối tượng người chơi:** Mọi lứa tuổi  

### Giới thiệu
Block Puzzle là game giải đố kéo thả block vào bảng 8x8 để hoàn thành hàng hoặc cột và xóa chúng nhằm ghi điểm và kéo dài thời gian chơi lâu nhất có thể.

### Mục tiêu thiết kế
- Lối chơi đơn giản, tập trung vào tư duy sắp xếp  
- Chơi liên tục không giới hạn thời gian  
- Trải nghiệm nhẹ, dễ tiếp cận  

---

## 2. Cấu trúc Scene
Game sử dụng 2 scene:

### Load Scene
- Hiển thị logo và loading  
- Khởi tạo dữ liệu game  
- Chuyển sang Gameplay Scene  

### Gameplay Scene
- Board chơi  
- UI gameplay  
- Popup Loss  
- Popup Setting  

---

## 3. Core Gameplay Loop
1. Sinh 3 block ngẫu nhiên  
2. Người chơi kéo thả block vào board  
3. Nếu đầy hàng hoặc cột thì thực hiện xóa  
4. Cộng điểm  
5. Sinh tiếp 3 block mới  
6. Tiếp tục cho đến khi không còn block nào có thể đặt  

---

## 4. Luật chơi
- Board mặc định 8x8  
- Block không có gravity  
- Block chỉ được đặt khi toàn bộ cell hợp lệ  
- Hoàn thành hàng hoặc cột để xóa  

---

## 5. Điều kiện thua
Game Over khi không có bất kỳ block nào trong 3 block hiện tại có thể đặt lên board.

---

## 6. Hệ thống điểm
### Điểm đặt block
- Điểm nhận được bằng số lượng cell của block  

Ví dụ:
- Block 1x1 → +1 điểm  
- Block 2x2 → +4 điểm  

### Điểm xóa hàng/cột
- Tính điểm dựa trên số hàng/cột bị xóa và combo  

---

## 7. Block System
### Các loại block
- 1x1  
- 1x2 / 2x1  
- 1x3 / 3x1  
- L-shape  
- T-shape  
- Square 2x2 / 3x3  

### Sinh block
- Mỗi lượt sinh 3 block  
- Block sinh ngẫu nhiên  
- Có thể điều chỉnh tỉ lệ xuất hiện  

---

## 8. UI
### In-game UI
- Score  
- Best Score  
- Khu vực chứa 3 block  
- Setting button  

### Popup
- Popup Loss  
- Popup Setting  

---

## 9. Công việc tôi thực hiện
- Đọc hiểu codebase hiện tại và gameplay flow  
- Xây dựng hệ thống **Virtual Board** mô phỏng trạng thái board hiện tại  
- Phát triển tính năng hỗ trợ người chơi khi board bị lấp trên 50%  

### Rescue Block Feature
- Copy trạng thái board hiện tại sang board ảo  
- Thử đặt block vào từng vị trí trên board ảo  
- Kiểm tra khả năng clear hàng/cột  
- Sau khi clear:
  - kiểm tra còn đủ không gian cho 2 block khác hay không  

Nếu tìm thấy trạng thái hợp lệ:
- Trả về:
  - 1 block có khả năng giải cứu  
  - 2 block khác có thể đặt tiếp  

Sau đó:
- Hoán đổi vị trí 3 block để người chơi không biết block nào là block hỗ trợ  

Nếu không tìm được:
- Trả về 3 block ngẫu nhiên  

### Block Variant System
- Xây dựng hệ thống tạo biến thể block từ block gốc:
  - Rotate  
  - Flip  

- Chuẩn hóa dữ liệu block sau transform  
- Kiểm tra block trùng lặp trước khi thêm vào danh sách block hợp lệ  

### Content Expansion
- Thêm block mới cho game  

---

## 10. Technical Challenges
### 1. Phân tích trạng thái board
- Mô phỏng trạng thái board hiện tại trên virtual board để kiểm tra khả năng đặt block mà không ảnh hưởng board thật  

### 2. Tìm kiếm block giải cứu
- Thử từng block tại từng vị trí hợp lệ  
- Kiểm tra khả năng clear hàng/cột  
- Mô phỏng trạng thái board sau clear  

### 3. Validate future moves
- Sau khi tìm được block có thể clear:
  - tiếp tục kiểm tra board còn đủ không gian cho 2 block khác  

Điều này giúp đảm bảo block hỗ trợ thực sự có thể cứu thế khó.

### 4. Block transformation
- Sinh các biến thể block bằng:
  - rotation  
  - flip  

- Chuẩn hóa dữ liệu để loại bỏ duplicate blocks.

### 5. Randomization balancing
- Hoán đổi vị trí block hỗ trợ để tránh người chơi nhận ra block cứu trợ.

---

## 11. Tech Stack
- Unity  
- C#  
- PlayerPrefs  
