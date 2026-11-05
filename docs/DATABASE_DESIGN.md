# Thiết kế cơ sở dữ liệu HomeEase

## 1. Trạng thái và nguyên tắc

Tài liệu này mô tả mô hình dữ liệu khái niệm cho PostgreSQL, dựa trên phạm vi hiện biết. PostgreSQL là cơ sở dữ liệu đã duyệt; backend sẽ dùng SQLAlchemy và Flask-Migrate. Đây chưa phải schema đã triển khai hoặc phê duyệt. Tên bảng, kiểu dữ liệu, ràng buộc, chỉ mục và quy tắc lưu trữ chi tiết đều cần được xác nhận; các mục chưa rõ được đánh dấu **TBD**.

Local development dự kiến chạy PostgreSQL bằng Docker Desktop và Docker Compose. Chưa có Compose file hoặc database container trong repository.

## 2. Thực thể khái niệm

| Thực thể | Mục đích | Quan hệ khái quát |
|---|---|---|
| Người dùng | Đại diện khách hàng hoặc quản trị viên; hỗ trợ xác thực và phân quyền. | Một người dùng có một vai trò hoặc các quyền; mô hình cụ thể **TBD**. |
| Vai trò/quyền | Phân biệt khách hàng và quản trị viên, giới hạn thao tác. | Gắn với người dùng; mô hình RBAC hay cách khác **TBD**. |
| Danh mục | Phân nhóm đồ gia dụng. | Có thể liên kết với nhiều sản phẩm; phân cấp **TBD**. |
| Sản phẩm | Thông tin đồ gia dụng có thể được duyệt và tìm kiếm. | Thuộc một hoặc nhiều danh mục; cardinality **TBD**. |
| Tồn kho | Ghi nhận lượng hàng của sản phẩm. | Liên kết với sản phẩm; có hỗ trợ nhiều kho hay không **TBD**. |
| Giỏ hàng | Tập hợp sản phẩm khách chọn trước checkout. | Gắn với người dùng hoặc phiên; chính sách **TBD**. |
| Mục giỏ hàng | Sản phẩm và số lượng trong giỏ. | Liên kết một giỏ hàng với một sản phẩm. |
| Đơn hàng | Ghi nhận yêu cầu mua, thông tin COD và trạng thái xử lý. | Có nhiều dòng đơn hàng; người mua có thể **TBD** theo chính sách đăng nhập. |
| Dòng đơn hàng | Sản phẩm và số lượng thuộc đơn hàng. | Liên kết đơn hàng với sản phẩm; lưu snapshot giá hay không **TBD**. |

Các thực thể về địa chỉ, lịch sử tồn kho, nhật ký quản trị, vận chuyển hoặc khuyến mãi chỉ được bổ sung nếu có quyết định nghiệp vụ tương ứng.

## 3. Danh mục sản phẩm

Danh mục cần bao gồm các nhóm đã yêu cầu: dụng cụ nấu ăn (cookware), nồi, chảo, bát, đĩa, đũa, thìa và dụng cụ nhà bếp.

Cách biểu diễn là các danh mục độc lập hay danh mục cha/con, mã định danh, nhãn tiếng Việt chính thức và việc một sản phẩm thuộc nhiều danh mục: **TBD**.

## 4. Thuộc tính cần xác định

Các thuộc tính dưới đây là những câu hỏi thiết kế, không phải danh sách cột đã chốt:

- Người dùng: định danh, thông tin đăng nhập, thông tin liên hệ, trạng thái và vai trò — trường cụ thể, dữ liệu cá nhân và cách bảo vệ: **TBD**.
- Sản phẩm: định danh, tên, mô tả, giá, hình ảnh, danh mục và trạng thái hiển thị — kiểu dữ liệu, tính bắt buộc và quy tắc giá: **TBD**.
- Tồn kho: số lượng hiện có, lượng giữ chỗ và lịch sử điều chỉnh — định nghĩa số lượng được tính và cách cập nhật: **TBD**.
- Giỏ hàng: chủ sở hữu/phiên, thời điểm hết hạn, các mục và số lượng — **TBD**.
- Đơn hàng: mã đơn, người đặt, thông tin người nhận, phương thức COD, tổng tiền và trạng thái — cấu trúc, thời điểm chốt dữ liệu và quy tắc tính tiền: **TBD**.
- Dòng đơn hàng: sản phẩm, số lượng, giá tại thời điểm đặt — lưu snapshot hay tham chiếu giá hiện tại: **TBD**.

## 5. Ràng buộc và nhất quán

- Định danh chính và khóa ngoại cần bảo đảm quan hệ giữa sản phẩm, danh mục, giỏ hàng và đơn hàng.
- Giá và số lượng cần có kiểu dữ liệu phù hợp, không dùng biểu diễn dấu phẩy động cho phép tính tiền.
- Cập nhật đơn hàng và tồn kho cần được thực hiện nhất quán theo chính sách đã chốt.
- Không giả định đơn hàng COD đã thanh toán khi mới được tạo.
- Quy tắc xóa, lưu trữ lịch sử, giá trị mặc định, ràng buộc duy nhất và xử lý dữ liệu không còn dùng: **TBD**.

Kiểu dữ liệu cụ thể, mức cô lập giao dịch, chiến lược khóa tồn kho, chỉ mục tìm kiếm và thời hạn lưu dữ liệu: **TBD**.

Khi thiết kế schema, giá trị tiền cần dùng kiểu decimal chính xác phù hợp với PostgreSQL/SQLAlchemy, không dùng số dấu phẩy động.

## 6. Quan hệ khái quát

```text
Người dùng ──< Giỏ hàng ──< Mục giỏ hàng >── Sản phẩm >── Danh mục
    │
    └──< Đơn hàng ──< Dòng đơn hàng >── Sản phẩm
                                      │
                                      └── Tồn kho
```

Sơ đồ thể hiện quan hệ khái niệm; số lượng quan hệ và mô hình kho cần được xác nhận.

## 7. Câu hỏi cần quyết định trước khi tạo schema

- Khách hàng có thể đặt hàng không cần tài khoản không?
- Sản phẩm thuộc một hay nhiều danh mục; danh mục có phân cấp không?
- Quản lý tồn kho theo một kho hay nhiều kho?
- Thời điểm giữ, trừ và hoàn tồn là khi nào?
- Đơn hàng lưu snapshot những thông tin nào để giữ lịch sử?
- Trạng thái đơn hàng/COD và chuyển trạng thái hợp lệ là gì?
- Chính sách xóa, lưu trữ và bảo vệ dữ liệu cá nhân ra sao?
- Có cần lịch sử điều chỉnh tồn kho hoặc nhật ký thao tác quản trị không?
