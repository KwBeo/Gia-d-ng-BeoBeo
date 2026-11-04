# Yêu cầu HomeEase

## 1. Mục đích và quy ước

Tài liệu ghi nhận phạm vi chức năng đã được nêu cho HomeEase, website thương mại điện tử đồ gia dụng. Những nội dung chưa có quyết định được đánh dấu **TBD** (chưa xác định), không được xem là yêu cầu đã được phê duyệt.

## 2. Vai trò

| Mã | Vai trò | Mô tả |
|---|---|---|
| R-CUS | Khách hàng | Người mua sắm, sử dụng tìm kiếm, bộ lọc, giỏ hàng và checkout. |
| R-ADM | Quản trị viên | Người quản lý nội dung sản phẩm, tồn kho và đơn hàng. |

Quy trình cấp tài khoản quản trị, quyền chi tiết, đăng ký khách hàng và quyền truy cập của người chưa đăng nhập: **TBD**.

## 3. Yêu cầu chức năng

### 3.1 Danh mục và sản phẩm

- **FR-PROD-01:** Hệ thống cần hỗ trợ sản phẩm đồ gia dụng thuộc các nhóm: dụng cụ nấu ăn, nồi, chảo, bát, đĩa, đũa, thìa và dụng cụ nhà bếp.
- **FR-PROD-02:** Khách hàng cần có thể duyệt và xem sản phẩm.
- **FR-PROD-03:** Khách hàng cần có thể tìm kiếm sản phẩm.
- **FR-PROD-04:** Khách hàng cần có thể lọc sản phẩm.
- **FR-PROD-05:** Quản trị viên cần có khả năng quản lý sản phẩm và danh mục.

Trường hiển thị, thuộc tính tìm kiếm, tiêu chí lọc, sắp xếp, phân trang, trạng thái sản phẩm và quy trình xuất bản: **TBD**.

### 3.2 Xác thực và phân quyền

- **FR-AUTH-01:** Hệ thống cần hỗ trợ xác thực và phân quyền.
- **FR-AUTH-02:** Hệ thống cần phân biệt vai trò khách hàng và quản trị viên.
- **FR-AUTH-03:** Các thao tác quản trị cần được giới hạn cho người có quyền phù hợp.

Phương thức đăng nhập, đăng ký, khôi phục tài khoản, thời hạn phiên, cách lưu thông tin xác thực, ma trận quyền và chính sách khóa tài khoản: **TBD**.

### 3.3 Giỏ hàng và checkout

- **FR-CART-01:** Khách hàng cần có thể thêm sản phẩm vào giỏ hàng.
- **FR-CART-02:** Khách hàng cần có thể xem và cập nhật giỏ hàng trước khi đặt hàng.
- **FR-CHECKOUT-01:** Hệ thống cần cung cấp luồng checkout để tạo đơn hàng.
- **FR-CHECKOUT-02:** Checkout cần hỗ trợ phương thức thanh toán COD.

Giỏ hàng gắn với tài khoản hay phiên khách, thông tin cần thu thập khi checkout, cách tính tổng tiền, xử lý giá thay đổi, tồn kho không đủ và chống đặt hàng lặp: **TBD**.

### 3.4 Đơn hàng và COD

- **FR-ORDER-01:** Hệ thống cần ghi nhận và quản lý đơn hàng.
- **FR-ORDER-02:** Đơn hàng cần ghi nhận việc chọn COD; không suy ra rằng đã thu tiền chỉ vì đơn được tạo.
- **FR-ORDER-03:** Quản trị viên cần có khả năng xem và quản lý đơn hàng.

Trạng thái đơn, chuyển trạng thái hợp lệ, thông tin người nhận, hủy đơn, hoàn hàng, xác nhận giao hàng và thời điểm ghi nhận thanh toán COD: **TBD**.

### 3.5 Tồn kho

- **FR-INV-01:** Hệ thống cần quản lý tồn kho sản phẩm.
- **FR-INV-02:** Các thay đổi đơn hàng và tồn kho cần được xử lý nhất quán theo quy tắc được thống nhất.
- **FR-INV-03:** Quản trị viên cần có khả năng quản lý tồn kho.

Thời điểm giữ/trừ/hoàn tồn, cho phép tồn âm, lịch sử điều chỉnh, cảnh báo hết hàng và phân quyền điều chỉnh: **TBD**.

## 4. Yêu cầu phi chức năng đã biết

- **NFR-01:** Giao diện hướng tới thiết kế hiện đại và đáp ứng trên nhiều kích thước màn hình.
- **NFR-02:** Ngôn ngữ nội dung hiển thị cho người dùng là tiếng Việt.
- **NFR-03:** Mật khẩu, khóa API và bí mật không được hardcode; cấu hình nhạy cảm sử dụng biến môi trường.
- **NFR-04:** Hệ thống cần có kiểm tra dữ liệu đầu vào và xử lý lỗi phù hợp.
- **NFR-05:** Tổ chức hệ thống tách biệt frontend, backend và cơ sở dữ liệu.

Mục tiêu hiệu năng, khả năng truy cập, trình duyệt hỗ trợ, yêu cầu sao lưu, bảo mật chi tiết, khả năng mở rộng và vận hành: **TBD**.

## 5. Quy tắc và giới hạn đã xác nhận

- Công nghệ định hướng: Next.js + TypeScript, Flask + Python và PostgreSQL.
- Phương thức thanh toán trong phạm vi hiện biết: COD.
- Chưa có phê duyệt cho cổng thanh toán điện tử hoặc yêu cầu nghiệp vụ khác ngoài các nội dung ở trên.

## 6. Tiêu chí nghiệm thu

Tiêu chí kiểm thử chi tiết cho từng yêu cầu, dữ liệu kiểm thử, mức độ bao phủ và người phê duyệt: **TBD**. Không xem các yêu cầu trong tài liệu này là đã triển khai nếu chưa được xác minh bằng kiểm thử.
