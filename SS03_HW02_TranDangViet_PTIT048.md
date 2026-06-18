# BÀI 2: Tối Ưu Hóa Prompt Đặc Tả Yêu Cầu Chức Năng

## Prompt hoàn chỉnh

### 1. Vai trò (Role)

Bạn là một **Senior Business Analyst / System Analyst** có hơn 10 năm kinh nghiệm trong việc xây dựng tài liệu SRS cho các hệ thống thương mại điện tử sử dụng **Spring Boot**, **JWT Authentication** và **RBAC (Role-Based Access Control)**.

### 2. Mục tiêu (Goal)

Hãy xây dựng tài liệu **Functional Requirements** cho chức năng **Authentication - Login** của dự án **Shop AI**.

Tài liệu phải mô tả đầy đủ quy trình xác thực người dùng, cấp phát JWT Token, kiểm tra quyền truy cập theo RBAC và xử lý các tình huống ngoại lệ thường gặp trong môi trường thực tế.

### 3. Ngữ cảnh (Context)

Shop AI là một nền tảng thương mại điện tử cho phép người dùng đăng nhập bằng email và mật khẩu đã đăng ký.

Sau khi xác thực thành công:

- Hệ thống tạo JWT Access Token.
- Người dùng sử dụng token này để truy cập các API được bảo vệ.
- Quyền truy cập được xác định thông qua mô hình RBAC.
- Hệ thống hiện có các vai trò: USER, STAFF và ADMIN.

Tài liệu cần mô tả:

- Mục tiêu nghiệp vụ của chức năng đăng nhập.
- Luồng xác thực người dùng.
- Cơ chế sinh và sử dụng JWT.
- Quy trình xác thực JWT ở các request tiếp theo.
- Cơ chế phân quyền theo RBAC.
- Các yêu cầu bảo mật liên quan đến Authentication.

### 4. Ràng buộc (Constraints)

Bắt buộc mô tả chi tiết các trường hợp ngoại lệ sau:

#### Trường hợp 1: Sai mật khẩu quá 5 lần

- Hệ thống phát hiện như thế nào.
- Tài khoản có bị khóa tạm thời hay không.
- Thời gian khóa đề xuất.
- Mã lỗi và thông báo trả về.

#### Trường hợp 2: JWT Token hết hạn

- Cách hệ thống phát hiện token hết hạn.
- HTTP Status Code trả về.
- Nội dung phản hồi lỗi.
- Hành động tiếp theo người dùng cần thực hiện.

#### Trường hợp 3: Tài khoản Inactive

- Thời điểm kiểm tra trạng thái tài khoản.
- Cách từ chối đăng nhập.
- Mã lỗi và thông báo phản hồi.

Ngoài ra:

- Không sinh mã nguồn Java.
- Không mô tả chi tiết implementation.
- Chỉ tập trung vào đặc tả nghiệp vụ.
- Các trường hợp ngoại lệ phải được mô tả riêng trong mục Exception Flow.
- Bổ sung các yêu cầu bảo mật liên quan đến JWT, RBAC và Account Lockout.

### 5. Định dạng đầu ra (Output Format)

Trình bày theo chuẩn SRS doanh nghiệp:

1. Functional Requirement Overview
2. Business Objective
3. Actors
4. Pre-conditions
5. Main Flow
6. Post-conditions
7. Exception Flow
   - Wrong Password (> 5 Attempts)
   - Expired JWT Token
   - Inactive Account Login Attempt

8. Security Requirements
9. Business Rules
10. Assumptions & Notes

Sử dụng văn phong chuyên nghiệp, rõ ràng, dễ đọc và phù hợp với tài liệu SRS thực tế của doanh nghiệp.
