# BÀI 2: Tối Ưu Hóa Prompt Đặc Tả Yêu Cầu Chức Năng

## Prompt đã tối ưu

```text
Vai trò (Role):
Bạn là một Senior Business Analyst có kinh nghiệm xây dựng tài liệu Software Requirements Specification (SRS) cho các hệ thống thương mại điện tử sử dụng JWT Authentication và Role-Based Access Control (RBAC).

Mục tiêu (Goal):
Hãy xây dựng tài liệu Functional Requirements cho chức năng Đăng nhập (Login) của dự án Shop AI.

Ngữ cảnh (Context):
Hệ thống Shop AI sử dụng JWT để xác thực người dùng và RBAC để phân quyền truy cập. Người dùng đăng nhập bằng email/tên đăng nhập và mật khẩu. Sau khi xác thực thành công, hệ thống phát hành JWT Token để sử dụng cho các yêu cầu tiếp theo. Quyền truy cập của người dùng được xác định dựa trên vai trò được gán trong hệ thống.

Ràng buộc (Constraints):
- Đặc tả đầy đủ luồng đăng nhập thành công.
- Mô tả rõ dữ liệu đầu vào, dữ liệu đầu ra và điều kiện tiền đề.
- Bắt buộc mô tả cách hệ thống xử lý các trường hợp ngoại lệ sau:
  1. Người dùng nhập sai mật khẩu quá 5 lần liên tiếp.
  2. JWT Token hết hạn trong khi phiên làm việc đang diễn ra.
  3. Tài khoản có trạng thái Inactive nhưng vẫn cố gắng đăng nhập.
- Mô tả phản hồi lỗi tương ứng cho từng trường hợp.
- Không bỏ sót các yêu cầu bảo mật liên quan đến JWT và RBAC.

Định dạng đầu ra (Output Format):
Trình bày theo cấu trúc Functional Requirements gồm:
1. Chức năng
2. Mô tả nghiệp vụ
3. Tiền điều kiện (Pre-conditions)
4. Luồng chính (Main Flow)
5. Luồng ngoại lệ (Exception Flow)
6. Dữ liệu đầu vào
7. Dữ liệu đầu ra
8. Quy tắc nghiệp vụ (Business Rules)
9. Yêu cầu bảo mật (Security Requirements)
```
