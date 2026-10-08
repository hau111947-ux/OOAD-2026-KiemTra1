# BÀI KIỂM TRA: PHÂN TÍCH VÀ THIẾT KẾ HỆ THỐNG QUẢN LÝ NHÀ HÀNG IT25
Tên: Đỗ Văn Hậu 
---
## I. MÔ TẢ YÊU CẦU BÀI TOÁN
Hệ thống quản lý nhà hàng IT25 cần đáp ứng các chức năng chính sau:
- **Quản lý thực đơn:** Gồm đồ ăn và đồ uống (Mã món, tên món, đơn giá, đơn vị tính, mô tả, ghi chú).
- **Quản lý nhân viên:** Mã nhân viên, tên nhân viên, giới tính, ngày sinh, số điện thoại, email, địa chỉ.
- **Tiếp nhận & Phục vụ khách tại quán:** Thu ngân nhập số bàn, tên khách, giờ gọi món, món ăn, ghi chú; hỗ trợ thêm, xoá, sửa món ăn khi có yêu cầu.
- **Đặt trước:** Khách hàng có thể liên hệ đặt bàn, đặt món trước khi đến.
- **Thanh toán:** Hỗ trợ thanh toán bằng tiền mặt hoặc qua ngân hàng (chuyển khoản/thẻ).
- **Kiểm toán ca:** Cuối ngày làm việc, thu ngân kiểm toán, đối chiếu tiền thực thu với tiền trên hệ thống và bàn giao cho quản lý.
- **Thống kê & Báo cáo:** Quản lý có thể thống kê doanh thu, lượt khách, các món bán chạy theo ngày, tuần hoặc tháng.
---
## II. SƠ ĐỒ USE-CASE
### 1. Hình ảnh sơ đồ Use-Case
*(Đặt ảnh bạn tự vẽ vào cùng thư mục với tên `usecase-diagram.png` hoặc cập nhật đúng đường dẫn bên dưới)*
![Sơ đồ Use-Case](usecase-diagram.png)
---
## III. MÔ TẢ CHI TIẾT 2 USE-CASE TIÊU BIỂU
### 1. Use-Case: Tiếp nhận và Gọi món (Order)
* **Mã Use-Case:** UC-01
* **Tác nhân (Actor):** Nhân viên thu ngân
* **Mục đích:** Ghi nhận thông tin gọi món, số bàn và các yêu cầu cụ thể của khách khi đến ăn tại nhà hàng.
* **Tiền điều kiện (Pre-condition):**
  * Nhân viên thu ngân đã đăng nhập thành công vào hệ thống.
  * Danh mục thực đơn và danh sách bàn đã được thiết lập sẵn trên hệ thống.
* **Hậu điều kiện (Post-condition):**
  * Một phiếu gọi món (Order/Hóa đơn tạm) mới được tạo thành công.
  * Trạng thái bàn được chuyển sang "Đang phục vụ".
* **Luồng sự kiện chính (Basic Flow):**
  1. Khách đến nhà hàng, nhân viên thu ngân mở giao diện tiếp nhận đơn mới.
  2. Thu ngân nhập thông tin: Số bàn, Tên khách hàng, Giờ gọi món.
  3. Thu ngân chọn các món ăn/đồ uống khách yêu cầu từ danh mục thực đơn, nhập số lượng và ghi chú riêng (nếu có).
  4. Hệ thống hiển thị danh sách món đã chọn và tự động tính tổng tiền tạm tính.
  5. Thu ngân xác nhận lưu đơn.
  6. Hệ thống lưu trữ đơn gọi món và cập nhật trạng thái bàn thành "Đang phục vụ".
* **Luồng sự kiện thay thế (Alternative Flow):**
  * *4a. Khách thay đổi yêu cầu trước khi chốt:* Thu ngân có thể thêm món, xoá bớt món hoặc chỉnh sửa số lượng trực tiếp trên danh sách trước khi xác nhận.
  * *4b. Món ăn đã hết:* Hệ thống cảnh báo món tạm ngưng phục vụ, thu ngân thông báo lại cho khách để đổi món khác.
---
### 2. Use-Case: Kiểm toán cuối ngày
* **Mã Use-Case:** UC-02
* **Tác nhân (Actor):** Nhân viên thu ngân, Quản lý nhà hàng
* **Mục đích:** Đối chiếu tổng tiền mặt và tiền chuyển khoản thực tế thu được trong ngày làm việc với dữ liệu ghi nhận trên phần mềm trước khi bàn giao tiền cho quản lý.
* **Tiền điều kiện (Pre-condition):**
  * Hết ca/ngày làm việc.
  * Tất cả hóa đơn trong ca đã được hoàn tất thanh toán hoặc đóng trạng thái.
* **Hậu điều kiện (Post-condition):**
  * Biên bản kiểm toán được lưu trữ thành công trên hệ thống.
  * Doanh thu được bàn giao hoàn tất cho Quản lý nhà hàng.
* **Luồng sự kiện chính (Basic Flow):**
  1. Thu ngân chọn chức năng "Kiểm toán cuối ngày".
  2. Hệ thống tổng hợp và hiển thị tổng số tiền ghi nhận trong ngày (chia theo 2 mục: Tiền mặt và Chuyển khoản ngân hàng).
  3. Thu ngân đếm số tiền mặt thực tế tại quầy và nhập số tiền này vào hệ thống.
  4. Hệ thống tự động so khớp, tính mức chênh lệch giữa số tiền thực thu và số tiền trên hệ thống (nếu có).
  5. Thu ngân tạo biên bản kiểm toán và gửi yêu cầu bàn giao cho Quản lý.
  6. Quản lý kiểm tra thực tế, xác nhận khớp dữ liệu và duyệt đóng ca làm việc.
* **Luồng sự kiện ngoại lệ (Exception Flow):**
  * *4a. Phát hiện chênh lệch tiền:* Thu ngân phải nhập lý do chênh lệch (thừa/thiếu tiền thối, hủy hóa đơn sai,...) vào ô ghi chú để quản lý xem xét và phê duyệt.

---

## IV. SƠ ĐỒ LỚP (CLASS DIAGRAM)

### 1. Hình ảnh sơ đồ Class Diagram
*(Đặt ảnh bạn tự vẽ vào cùng thư mục với tên `class-diagram.png` hoặc cập nhật đúng đường dẫn bên dưới)*

![Sơ đồ Class Diagram](class-diagram.png)

---

## V. GIẢI THÍCH LỚP KẾT HỢP (ASSOCIATION CLASS)

### Lớp kết hợp: `ChiTietHoaDon` (Order Detail / Invoice Detail)
* **Bản chất mối quan hệ gốc:**
  * Giữa lớp **`HoaDon`** (Hóa đơn) và lớp **`MonAn`** (Món ăn) tồn tại mối quan hệ **Nhiều - Nhiều ($N - N$)**:
    * Một hóa đơn có thể chứa nhiều món ăn khác nhau.
    * Một món ăn có thể xuất hiện trong nhiều hóa đơn của các bàn/khách hàng khác nhau.
* **Lý do hình thành lớp kết hợp `ChiTietHoaDon`:**
  * Trong thực tế, khi khách gọi một món ăn vào một hóa đơn, sẽ phát sinh các thuộc tính phụ thuộc đồng thời vào cả hai thực thể:
    * `soLuong` (Số lượng đĩa/ly được gọi).
    * `donGiaBan` (Đơn giá thực tế tại thời điểm xuất bill – đề phòng giá niêm yết của món ăn thay đổi sau này).
    * `ghiChu` (Yêu cầu riêng của khách: ít đá, không cay, không đường...).
  * Các thuộc tính này không thể đặt riêng ở lớp `MonAn` (vì mỗi bàn khách gọi số lượng và ghi chú khác nhau), cũng không thể đặt trực tiếp ở lớp `HoaDon` (vì một hóa đơn có nhiều món với các số lượng khác nhau).
* **Vai trò:**
  * Lớp `ChiTietHoaDon` đóng vai trò là một **Association Class** (lớp kết hợp) để phân rã mối quan hệ nhiều - nhiều ($N - N$) thành hai quan hệ một - nhiều ($1 - N$):
    * `HoaDon (1) --- (1..*) ChiTietHoaDon`
    * `MonAn (1) --- (0..*) ChiTietHoaDon`
  * Đồng thời, nó chịu trách nhiệm tính toán tiền thành phần cho từng món qua phương thức:  
    $$\text{thanhTien} = \text{soLuong} \times \text{donGiaBan}$$
