# Kế hoạch phát triển HomeEase

## 1. Mục đích

Kế hoạch này chia nhỏ việc phát triển website thương mại điện tử đồ gia dụng HomeEase thành các giai đoạn phụ thuộc lẫn nhau. Đây là thứ tự công việc định hướng, không phải cam kết ngày hoàn thành hoặc phê duyệt triển khai. Ước lượng, nhân sự, lịch phát hành và tiêu chí nghiệm thu: **TBD**.

## 2. Các giai đoạn đề xuất

### Giai đoạn 1 — Chốt yêu cầu và quyết định còn thiếu

- Xác nhận luồng khách hàng và quản trị viên.
- Chốt chính sách đăng nhập/đặt hàng, quyền quản trị và tiêu chí nghiệm thu.
- Chốt quy tắc danh mục, tìm kiếm/lọc, giá, checkout COD, tồn kho và đơn hàng.
- Xác nhận các mục **TBD** trong tài liệu yêu cầu, dữ liệu và API.

**Điều kiện chuyển tiếp:** Các quyết định ảnh hưởng đến schema và API được thống nhất.

### Giai đoạn 2 — Thiết lập nền tảng dự án

- Tổ chức frontend Node.js 24 LTS/npm/Next.js stable App Router/TypeScript strict mode/Tailwind CSS/ESLint, backend Python 3.13/Flask 3.x/SQLAlchemy/Flask-Migrate và PostgreSQL thành các phần tách biệt.
- Thống nhất cấu hình theo môi trường, quy ước mã nguồn, kiểm tra đầu vào và xử lý lỗi.
- Thiết lập quy trình chạy ứng dụng và kiểm thử phù hợp với môi trường của nhóm bằng Docker Desktop/Docker Compose cho PostgreSQL.

Các lựa chọn stack ở trên đã được duyệt và cố định trừ khi chủ dự án phê duyệt thay đổi. Repository hiện chưa có application scaffold, manifest dependencies hoặc Compose file.

### Giai đoạn 3 — Xác thực, vai trò và dữ liệu sản phẩm

- Xây dựng xác thực và phân quyền khách hàng/quản trị viên theo chính sách đã duyệt.
- Xây dựng cấu trúc danh mục và sản phẩm gồm các nhóm đồ gia dụng đã xác nhận.
- Cung cấp khả năng quản trị sản phẩm/danh mục theo ma trận quyền.

Chi tiết về quy trình tài khoản và vòng đời sản phẩm: phụ thuộc quyết định giai đoạn 1.

### Giai đoạn 4 — Duyệt, tìm kiếm và lọc sản phẩm

- Xây dựng giao diện duyệt và xem chi tiết sản phẩm.
- Xây dựng API và giao diện tìm kiếm/lọc theo tiêu chí đã được duyệt.
- Kiểm tra hiển thị đáp ứng và nội dung tiếng Việt.

### Giai đoạn 5 — Giỏ hàng và checkout COD

- Xây dựng luồng giỏ hàng.
- Xây dựng checkout và tạo đơn COD.
- Kiểm thử dữ liệu đầu vào, giá và tồn kho theo quy tắc nghiệp vụ đã chốt.

### Giai đoạn 6 — Quản lý đơn hàng và tồn kho

- Xây dựng giao diện/API tra cứu và quản lý đơn hàng.
- Xây dựng cập nhật tồn kho và các quy tắc nhất quán đã được phê duyệt.
- Kiểm thử các chuyển trạng thái, tình huống lỗi và cập nhật đồng thời theo yêu cầu đã chốt.

### Giai đoạn 7 — Kiểm thử, hoàn thiện và bàn giao

- Kiểm thử tích hợp frontend, backend và PostgreSQL.
- Kiểm thử luồng chính theo vai trò, COD, tồn kho, tìm kiếm và bộ lọc.
- Rà soát quyền truy cập, thông báo lỗi, giao diện đáp ứng và nội dung tiếng Việt.
- Cập nhật tài liệu, ghi nhận phần chưa hoàn thành và chuẩn bị trình diễn/bàn giao.

Phạm vi tự động hóa kiểm thử và môi trường bàn giao: **TBD**.

## 3. Nguyên tắc thực hiện

- Làm rõ yêu cầu trước khi đưa quyết định nghiệp vụ vào mã nguồn hoặc schema.
- Giữ frontend, backend và dữ liệu tách biệt; xác thực quyền ở backend.
- Không đưa bí mật vào mã nguồn; dùng cấu hình môi trường và mẫu an toàn.
- Mỗi thay đổi chức năng cần có kiểm thử liên quan trước khi tuyên bố hoàn tất.
- Không coi các tính năng ngoài phạm vi đã xác nhận là phần việc mặc định.

## 4. Phụ thuộc và rủi ro cần giải quyết

- Quy tắc tồn kho chưa rõ có thể ảnh hưởng đến giao dịch checkout và thiết kế dữ liệu.
- Chính sách đặt hàng khi chưa đăng nhập ảnh hưởng đến tài khoản, giỏ hàng và truy vấn đơn.
- Vòng đời đơn/COD chưa chốt ảnh hưởng đến thao tác quản trị và trạng thái thanh toán.
- Tiêu chí tìm kiếm/lọc chưa chốt ảnh hưởng đến giao diện, API và chỉ mục dữ liệu.
- Hạ tầng, lịch làm việc và nguồn lực nhóm: **TBD**.

## 5. Theo dõi tiến độ

Trạng thái từng giai đoạn, người phụ trách, thời hạn, định nghĩa hoàn thành và cách quản lý thay đổi: **TBD**. Cập nhật tiến độ sau khi nhóm thống nhất kế hoạch thực thi.

## 6. Thiết lập phát triển local

### 6.1 Công cụ cần có

- Git và quyền truy cập repository trên GitHub.
- Node.js 24 LTS và npm.
- Python 3.13.
- Docker Desktop có Docker Compose.

Kiểm tra phiên bản sau khi cài công cụ:

```powershell
git --version
node --version
npm --version
python --version
docker --version
docker compose version
```

### 6.2 Quy trình dự kiến sau khi scaffold

Các bước này mô tả quy trình mục tiêu; một số file được tham chiếu chưa tồn tại và chưa thể chạy ở trạng thái repository hiện tại.

1. Tạo/đi vào virtual environment backend từ thư mục repository:

   ```powershell
   python -m venv backend\.venv
   .\backend\.venv\Scripts\Activate.ps1
   ```

2. Cài dependencies backend từ manifest/lock đã được thêm ở giai đoạn scaffold; tên và định dạng file dependency sẽ được thống nhất khi scaffold.
3. Cài dependencies frontend bằng `npm install` trong `frontend/` sau khi `package.json` và lockfile được tạo.
4. Sao chép các file `.env.example` tương ứng thành file `.env` local và điền giá trị chỉ dùng trên máy phát triển. Không commit file `.env` hoặc bí mật.
5. Khởi chạy PostgreSQL bằng `docker compose up -d` từ thư mục có `compose.yaml`. Compose file và tên service hiện chưa được tạo; không chạy container cho đến khi file được phê duyệt/đưa vào repository.
6. Chạy database migration bằng Flask-Migrate sau khi ứng dụng Flask, cấu hình database và migration đầu tiên được tạo.
7. Chạy frontend/backend bằng scripts/entry points do scaffold tạo ra. Tên lệnh, cổng và health check sẽ được ghi lại khi chúng tồn tại.

Không giả định ứng dụng, migration, `.env.example`, `compose.yaml` hoặc dependencies đã tồn tại. Không chạy lệnh cài đặt hay khởi tạo container như một phần của bước tài liệu này.

## 7. Quy trình Git và GitHub

1. `develop` là nhánh tích hợp; `main` dành cho các bản phát hành theo quyết định của nhóm.
2. Trước khi bắt đầu, kiểm tra `git status` và cập nhật `develop` từ remote bằng fast-forward.
3. Tạo nhánh riêng từ `develop` theo quy ước `feature/<feature-name>`, `fix/<bug-name>` hoặc `docs/<document-name>`.
4. Thực hiện thay đổi, chạy kiểm tra liên quan và mở Pull Request trên GitHub hướng vào `develop`.
5. Không làm việc trực tiếp trên `main`/`develop`; không commit hoặc push trừ khi được yêu cầu rõ ràng.
6. Chỉ đưa thay đổi từ `develop` sang `main` theo quy trình phát hành được nhóm thống nhất.

Ví dụ bắt đầu nhánh tài liệu trong PowerShell:

```powershell
git switch develop
git pull --ff-only
git switch -c docs/project-setup
```

Sau khi có `package.json` và `package-lock.json`, ưu tiên `npm ci` trong `frontend/` để cài đúng dependencies đã khóa. Sau khi backend có `requirements.txt`, cài bằng `python -m pip install -r backend\requirements.txt` trong virtual environment. Các file dependency này chưa tồn tại và chưa được tạo trong bước tài liệu.
