# Tài liệu API HomeEase

## 1. Trạng thái tài liệu

Tài liệu này là bản định hướng API cho kiến trúc Next.js, Flask và PostgreSQL. Chưa có API được xác nhận là đã triển khai. Đường dẫn và phương thức bên dưới là **đề xuất để thảo luận**, không phải hợp đồng API đã phê duyệt. Phiên bản, schema request/response, mã lỗi và chi tiết xác thực: **TBD**.

## 2. Quy ước chung cần thống nhất

- Frontend giao tiếp với backend Flask qua API.
- Nội dung người dùng hiển thị bằng tiếng Việt; tên trường API có thể theo quy ước kỹ thuật thống nhất sau.
- Backend cần xác thực dữ liệu đầu vào, danh tính và quyền truy cập.
- Không trả thông tin bí mật hoặc thông tin xác thực nhạy cảm trong phản hồi.
- Định dạng lỗi, phân trang, sắp xếp, lọc, định dạng ngày giờ và tiền tệ: **TBD**.
- Cơ chế xác thực (cookie/session hay token), CSRF, CORS và thời hạn phiên: **TBD**.

## 3. Nhóm endpoint dự kiến

Các route dưới đây là ví dụ cấu trúc để xác định phạm vi API. Cần được rà soát và phê duyệt trước khi triển khai.

| Phương thức | Đường dẫn dự kiến | Vai trò dự kiến | Mục đích |
|---|---|---|---|
| GET | `/api/products` | Công khai theo chính sách truy cập **TBD** | Liệt kê, tìm kiếm và lọc sản phẩm. |
| GET | `/api/products/{product_id}` | Công khai theo chính sách truy cập **TBD** | Xem chi tiết sản phẩm. |
| GET | `/api/categories` | Công khai theo chính sách truy cập **TBD** | Liệt kê danh mục. |
| POST | `/api/auth/login` | Khách hàng/quản trị viên | Xác thực người dùng; phương thức và body **TBD**. |
| POST | `/api/auth/logout` | Người dùng đã xác thực | Kết thúc phiên nếu áp dụng; chi tiết **TBD**. |
| GET | `/api/cart` | Khách hàng hoặc phiên khách **TBD** | Xem giỏ hàng. |
| POST | `/api/cart/items` | Khách hàng hoặc phiên khách **TBD** | Thêm sản phẩm vào giỏ. |
| PATCH | `/api/cart/items/{item_id}` | Chủ giỏ hàng **TBD** | Cập nhật mục giỏ hàng. |
| DELETE | `/api/cart/items/{item_id}` | Chủ giỏ hàng **TBD** | Xóa mục khỏi giỏ hàng. |
| POST | `/api/orders` | Khách hàng; yêu cầu đăng nhập **TBD** | Checkout và tạo đơn hàng COD. |
| GET | `/api/orders` | Khách hàng/quản trị viên theo quyền **TBD** | Xem danh sách đơn hàng phù hợp với quyền. |
| GET | `/api/orders/{order_id}` | Chủ đơn/quản trị viên theo quyền **TBD** | Xem chi tiết đơn. |
| GET/POST/PATCH | `/api/admin/products` và `/api/admin/products/{product_id}` | Quản trị viên | Quản lý sản phẩm; các thao tác cụ thể cần chốt. |
| GET/PATCH | `/api/admin/inventory` và `/api/admin/inventory/{product_id}` | Quản trị viên | Xem hoặc điều chỉnh tồn kho theo chính sách **TBD**. |
| GET/PATCH | `/api/admin/orders` và `/api/admin/orders/{order_id}` | Quản trị viên | Tra cứu và cập nhật đơn hàng theo chuyển trạng thái hợp lệ **TBD**. |

Endpoint quản lý danh mục, đăng ký, hồ sơ, tìm kiếm nâng cao, lịch sử đơn và các thao tác khác: **TBD**.

## 4. Tham số tìm kiếm và lọc

`GET /api/products` có thể hỗ trợ tham số truy vấn tìm kiếm và lọc. Tên tham số, trường được tìm, tiêu chí lọc (bao gồm danh mục), sắp xếp, giới hạn kết quả và định dạng phản hồi đều **TBD**.

Không nên coi một bộ lọc theo giá, thương hiệu, đánh giá hay trạng thái còn hàng là yêu cầu đã phê duyệt nếu chưa có quyết định.

## 5. Checkout và COD

API tạo đơn cần nhận dữ liệu checkout đã được xác định, xác nhận phương thức COD và trả kết quả tạo đơn. Trường thông tin người nhận, địa chỉ, nội dung giỏ hàng được lấy từ client hay server, cách tính tiền, xử lý giá/tồn kho thay đổi và tính lặp an toàn của yêu cầu (idempotency): **TBD**.

Backend cần tự kiểm tra lại sản phẩm, giá và tồn kho theo quy tắc đã thống nhất; không tin tổng tiền do client tự gửi. Quy tắc cụ thể phải được chốt trước khi triển khai.

## 6. Phân quyền

- API đọc sản phẩm/danh mục có cần đăng nhập hay không: **TBD**.
- API giỏ hàng chỉ cho chủ sở hữu hoặc phiên tương ứng truy cập: cơ chế xác định chủ sở hữu **TBD**.
- API đơn hàng giới hạn theo quyền và chủ thể phù hợp: quy tắc cụ thể **TBD**.
- API `/api/admin/*` chỉ dành cho quản trị viên được cấp quyền: ma trận quyền và kiểm soát quyền thực tế **TBD**.

## 7. Lỗi và mã trạng thái

Schema phản hồi lỗi, mã lỗi nghiệp vụ, ánh xạ HTTP status, thông báo cho người dùng và cách xử lý lỗi xác thực/ủy quyền: **TBD**. Phản hồi không được làm lộ bí mật hoặc chi tiết nội bộ.

## 8. Cần hoàn thiện trước khi API được xem là hợp đồng

- Phê duyệt route, phương thức và quyền.
- Chốt schema request/response và quy ước trường.
- Định nghĩa lỗi và status code.
- Chốt cơ chế xác thực, CORS/CSRF và phiên.
- Xác định quy tắc tồn kho, giá và trạng thái đơn trong checkout.
- Viết kiểm thử hợp đồng API sau khi có schema được duyệt.

