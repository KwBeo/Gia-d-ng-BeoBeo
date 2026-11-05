# Kiến trúc hệ thống HomeEase

## 1. Trạng thái tài liệu

Đây là mô tả kiến trúc mục tiêu dựa trên công nghệ và phạm vi đã cung cấp. Stack dưới đây đã được chủ dự án duyệt; tài liệu không xác nhận rằng mã nguồn, dịch vụ triển khai hay container đã tồn tại. Các lựa chọn nghiệp vụ/kỹ thuật chi tiết chưa được quyết định được đánh dấu **TBD**.

## 2. Stack đã duyệt

- Frontend: Node.js 24 LTS, npm, Next.js stable, App Router, TypeScript strict mode, Tailwind CSS và ESLint.
- Backend: Python 3.13, Flask 3.x, pip/`venv`, SQLAlchemy, Flask-Migrate và REST API.
- Database và local services: PostgreSQL chạy qua Docker Desktop/Docker Compose.
- Git/GitHub cho quản lý phiên bản và cộng tác.

Các lựa chọn này cố định trừ khi có phê duyệt thay đổi rõ ràng. Phiên bản patch Next.js stable được chọn ở bước scaffold.

## 3. Sơ đồ khái quát

```text
Trình duyệt khách hàng/quản trị viên
                |
                v
Frontend: Next.js + TypeScript
                |
        Giao tiếp qua API
                |
                v
Backend: Python + Flask
                |
        Truy cập dữ liệu
                |
                v
Database: PostgreSQL
```

Giao thức, địa chỉ triển khai, cơ chế giao tiếp bổ sung và cách lưu tệp/hình ảnh: **TBD**.

## 4. Trách nhiệm các thành phần

### 4.1 Frontend

Next.js và TypeScript chịu trách nhiệm giao diện tiếng Việt, hiển thị danh mục/sản phẩm, tìm kiếm và lọc, giỏ hàng, checkout COD, cùng giao diện quản trị phù hợp với quyền người dùng.

Tailwind CSS là lựa chọn đã duyệt cho styling; ESLint là lựa chọn đã duyệt cho linting. Quyết định về kết xuất trang, quản lý trạng thái, lưu trữ dữ liệu giỏ hàng và tổ chức route: **TBD**.

### 4.2 Backend

Python và Flask cung cấp API cho các luồng ứng dụng. Backend là nơi thực hiện xác thực và kiểm tra quyền, kiểm tra dữ liệu đầu vào, xử lý nghiệp vụ sản phẩm, giỏ hàng, checkout, đơn hàng và tồn kho, cũng như truy cập cơ sở dữ liệu.

Cấu trúc module, thư viện xác thực, phiên bản API, quy ước lỗi và cách xử lý giao dịch: **TBD**. SQLAlchemy quản lý truy cập dữ liệu; Flask-Migrate quản lý migration. Định hướng endpoint được ghi tại [Tài liệu API](./API_DOCUMENTATION.md).

### 4.3 Cơ sở dữ liệu

PostgreSQL lưu trữ dữ liệu có cấu trúc như tài khoản, sản phẩm, danh mục, tồn kho, giỏ hàng và đơn hàng theo mô hình được thống nhất. Mô hình dưới đây ở mức khái niệm, chưa phải schema đã triển khai.

Chi tiết xem [Thiết kế cơ sở dữ liệu](./DATABASE_DESIGN.md).

## 5. Nguyên tắc phân lớp

- Frontend trình bày dữ liệu và gửi yêu cầu; không tự quyết định quyền truy cập hay trạng thái đơn hàng.
- Backend kiểm tra dữ liệu và quyền, thực thi quy tắc nghiệp vụ, rồi truy cập cơ sở dữ liệu.
- PostgreSQL lưu dữ liệu bền vững; mọi thay đổi liên quan đơn hàng và tồn kho cần có quy tắc nhất quán được xác định.
- Bí mật cấu hình được cung cấp qua môi trường chạy, không nhúng vào mã nguồn.
- Trách nhiệm frontend, backend và dữ liệu được tách biệt để thuận tiện bảo trì và kiểm thử.

Các quy tắc cụ thể về giao dịch, ranh giới module và triển khai: **TBD**.

## 6. Luồng nghiệp vụ khái quát

### 6.1 Duyệt và tìm sản phẩm

1. Khách hàng yêu cầu danh sách sản phẩm hoặc tìm kiếm/lọc.
2. Frontend gửi yêu cầu đến API.
3. Backend kiểm tra tham số và truy vấn dữ liệu sản phẩm.
4. Frontend hiển thị kết quả.

Trường tìm kiếm và bộ lọc chính thức: **TBD**.

### 6.2 Checkout COD

1. Khách hàng kiểm tra giỏ hàng và gửi yêu cầu checkout.
2. Backend xác thực người dùng theo chính sách đã chốt, kiểm tra dữ liệu và khả năng đáp ứng tồn kho.
3. Backend tạo đơn hàng với phương thức COD theo quy tắc giao dịch đã xác định.
4. Frontend hiển thị kết quả đặt hàng.

Thứ tự giữ/trừ tồn, dữ liệu người nhận, xử lý lỗi một phần và định dạng xác nhận: **TBD**.

### 6.3 Quản trị

1. Quản trị viên xác thực.
2. Backend kiểm tra quyền cho thao tác quản trị.
3. Quản trị viên thao tác với sản phẩm, tồn kho hoặc đơn hàng qua frontend.
4. Backend xác thực đầu vào và ghi nhận thay đổi.

Ma trận quyền, nhật ký kiểm toán và quy trình duyệt: **TBD**.

## 7. Bảo mật và xử lý lỗi

- Xác thực danh tính và kiểm tra quyền ở backend.
- Không tin dữ liệu do client gửi; kiểm tra ở ranh giới API.
- Không ghi mật khẩu hay bí mật vào mã nguồn hoặc phản hồi API.
- Trả lỗi theo định dạng nhất quán, tránh làm lộ thông tin nhạy cảm.

Chi tiết về mã hóa mật khẩu, quản lý phiên/token, giới hạn yêu cầu, ghi log và chính sách lưu dữ liệu: **TBD**.

## 8. Phát triển local

Thiết lập máy local dự kiến sử dụng Node.js 24 LTS/npm, Python 3.13/`venv`/pip và PostgreSQL qua Docker Desktop/Docker Compose. Các lệnh và trạng thái hiện tại được ghi trong [Kế hoạch phát triển](./DEVELOPMENT_PLAN.md). Chưa có package manifest, mã nguồn ứng dụng hoặc Compose file.

## 9. Triển khai và vận hành

Nhà cung cấp máy chủ, môi trường phát triển/kiểm thử/sản xuất, CI/CD, giám sát, sao lưu, cấu hình tên miền và cách phục vụ media: **TBD**.
