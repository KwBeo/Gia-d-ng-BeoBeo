# Backend HomeEase

## Stack đã duyệt

- Python 3.13 với `venv` và pip
- Flask 3.x và REST API
- SQLAlchemy để truy cập dữ liệu
- Flask-Migrate để quản lý database migration
- PostgreSQL làm cơ sở dữ liệu

Quy tắc nghiệp vụ và truy cập dữ liệu thuộc backend; cần kiểm tra dữ liệu đầu
vào và thực thi quyền ở ranh giới API. Không đưa thông tin xác thực hoặc cấu
hình riêng của môi trường vào source control.

## Trạng thái hiện tại

Thư mục này hiện chỉ có tài liệu setup. Mã nguồn ứng dụng, manifest
dependencies, migration và packages chưa được tạo. Xem
[`../docs/DEVELOPMENT_PLAN.md`](../docs/DEVELOPMENT_PLAN.md) để biết quy trình
phát triển local dự kiến.
