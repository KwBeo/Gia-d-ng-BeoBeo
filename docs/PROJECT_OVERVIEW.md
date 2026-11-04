# Tổng quan dự án HomeEase

## 1. Giới thiệu

HomeEase là website thương mại điện tử về đồ gia dụng, tập trung vào các sản phẩm phục vụ nhà bếp. Đây là dự án phần mềm trong khuôn khổ học phần đại học. Tài liệu này mô tả định hướng hiện tại, không khẳng định các chức năng đã được triển khai.

## 2. Mục tiêu

- Hỗ trợ khách hàng tìm kiếm, xem và chọn mua đồ gia dụng.
- Cung cấp luồng giỏ hàng và thanh toán bằng hình thức trả tiền khi nhận hàng (Cash on Delivery — COD).
- Hỗ trợ quản trị viên quản lý sản phẩm, tồn kho và đơn hàng.
- Xây dựng giao diện hiện đại, đáp ứng nhiều kích thước màn hình; nội dung hiển thị cho người dùng bằng tiếng Việt.

Phạm vi chi tiết và tiêu chí nghiệm thu: **TBD**.

## 3. Người dùng và vai trò

| Vai trò | Mục đích sử dụng |
|---|---|
| Khách hàng | Duyệt và tìm sản phẩm, sử dụng giỏ hàng, thực hiện đặt hàng COD và theo dõi đơn hàng. |
| Quản trị viên | Quản lý sản phẩm, danh mục, tồn kho và đơn hàng; quyền cụ thể cho từng thao tác là **TBD**. |

Khách có thể xem sản phẩm mà không đăng nhập hay không, và các thao tác nào bắt buộc đăng nhập: **TBD**.

## 4. Danh mục sản phẩm

Phạm vi danh mục được yêu cầu bao gồm:

- Dụng cụ nấu ăn (cookware)
- Nồi
- Chảo
- Bát
- Đĩa
- Đũa
- Thìa
- Dụng cụ nhà bếp

Cách phân cấp danh mục, tên gọi hiển thị chính thức, thuộc tính sản phẩm và quy tắc phân loại: **TBD**.

## 5. Chức năng trong phạm vi định hướng

- Duyệt danh sách và xem thông tin sản phẩm.
- Tìm kiếm và lọc sản phẩm; trường tìm kiếm, tiêu chí lọc, sắp xếp và phân trang: **TBD**.
- Quản lý giỏ hàng và thực hiện checkout.
- Đặt hàng với phương thức COD.
- Quản lý đơn hàng và tồn kho.
- Xác thực người dùng và phân quyền khách hàng/quản trị viên.

Quy tắc giá, vận chuyển, hủy/đổi trả, tồn kho khi đặt hàng và vòng đời đơn hàng chưa được xác định; xem [Yêu cầu](./REQUIREMENTS.md).

## 6. Công nghệ định hướng

- Frontend: Next.js và TypeScript.
- Backend: Python và Flask.
- Cơ sở dữ liệu: PostgreSQL.

Đây là kiến trúc mục tiêu theo thông tin dự án, không phải xác nhận rằng các thành phần đã có trong mã nguồn. Phiên bản, cách triển khai và môi trường chạy: **TBD**. Mô tả ở [Kiến trúc hệ thống](./SYSTEM_ARCHITECTURE.md).

## 7. Ngoài phạm vi đã xác nhận

Chưa có quyết định xác nhận các tính năng như thanh toán trực tuyến, khuyến mãi, đánh giá sản phẩm, vận chuyển tích hợp hoặc nhiều ngôn ngữ. Không coi các tính năng này là yêu cầu cho đến khi được phê duyệt.

## 8. Tài liệu liên quan

- [Yêu cầu](./REQUIREMENTS.md)
- [Kiến trúc hệ thống](./SYSTEM_ARCHITECTURE.md)
- [Thiết kế cơ sở dữ liệu](./DATABASE_DESIGN.md)
- [Tài liệu API](./API_DOCUMENTATION.md)
- [Kế hoạch phát triển](./DEVELOPMENT_PLAN.md)
- [Nhật ký thay đổi](./CHANGELOG.md)
