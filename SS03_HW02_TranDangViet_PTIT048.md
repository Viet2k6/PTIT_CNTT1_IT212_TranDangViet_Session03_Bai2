# Bài 2: Tối Ưu Hóa Prompt Đặc Tả Yêu Cầu Chức Năng

## 1. Yêu Cầu Bài Tập

## Thiết kế lại prompt để sinh tài liệu Functional Requirements cho module Đăng nhập của dự án Shop AI (dùng JWT và RBAC). Prompt phải tuân thủ cấu trúc 5 thành phần và có cài cắm bẫy dữ liệu (Edge Cases).

## 2. Phần 1: Prompt Tối Ưu

Dưới đây là prompt đã được thiết kế lại, tuân thủ nghiêm ngặt cấu trúc 5 thành phần (Vai trò, Mục tiêu, Ngữ cảnh, Ràng buộc, Định dạng):

```text
[Vai trò]
Bạn là một Chuyên viên Phân tích Nghiệp vụ (Business Analyst - BA) dày dặn kinh nghiệm, chuyên thiết kế tài liệu đặc tả yêu cầu phần mềm cho các hệ thống thương mại điện tử quy mô lớn.
[Mục tiêu]
Nhiệm vụ của bạn là viết một tài liệu Yêu cầu chức năng (Functional Requirements) chi tiết và khắt khe cho module "Đăng nhập" (Authentication) của dự án "Shop AI".
[Ngữ cảnh]
Hệ thống "Shop AI" đang được xây dựng dựa trên tiêu chuẩn bảo mật rất cao. Module xác thực này sử dụng công nghệ JSON Web Token (JWT) để quản lý phiên làm việc và áp dụng mô hình phân quyền dựa trên vai trò (Role-Based Access Control - RBAC).
[Ràng buộc]
Tài liệu cần phải đặc tả rõ ràng cách hệ thống xử lý triệt để 3 trường hợp ngoại lệ (Edge Cases) sau:
1. Người dùng nhập sai mật khẩu quá 5 lần.
2. Token JWT hết hạn (expired) trong lúc phiên làm việc đang diễn ra.
3. Tài khoản người dùng ở trạng thái khóa (Inactive) nhưng cố tình thực hiện đăng nhập.
Tuyệt đối không được bỏ sót bất kỳ trường hợp nào. Đối với mỗi trường hợp, phải đưa ra luồng xử lý (flow) chi tiết của hệ thống hoặc thông báo lỗi (error message) cụ thể hiển thị cho người dùng.
[Định dạng]
Trình bày tài liệu dưới dạng văn bản Markdown. Sử dụng các tiêu đề rõ ràng (Heading), danh sách gạch đầu dòng (Bullet points) để phân cấp các yêu cầu nghiệp vụ, phân chia rõ luồng xử lý chính (Happy path) và luồng xử lý ngoại lệ.
```

---

## 3. Phần 2: Phản Hồi Của AI (Kết quả chạy thử nghiệm)

Dưới đây là phản hồi của AI khi chạy prompt trên để cung cấp làm minh chứng thực nghiệm:

```text
# Tài Liệu Yêu Cầu Chức Năng (Functional Requirements)
## Module: Đăng nhập (Authentication)
## Dự án: Shop AI
### 1. Giới thiệu
Tài liệu này cung cấp đặc tả yêu cầu chức năng cho Module Đăng nhập của hệ thống Shop AI. Module đóng vai trò cổng gác bảo mật, sử dụng chuẩn JWT để quản lý phiên làm việc và RBAC để thực thi phân quyền người dùng.
### 2. Yêu cầu chức năng chính (Happy Path)
- **FR1.01**: Hệ thống cho phép người dùng cung cấp Tên đăng nhập (Username/Email) và Mật khẩu để xác thực.
- **FR1.02**: Khi thông tin hợp lệ, hệ thống sinh ra một Access Token (JWT) và một Refresh Token.
- **FR1.03**: Hệ thống phân tích Role từ dữ liệu người dùng để áp dụng mô hình RBAC và trả về thông tin phân quyền kèm theo dữ liệu phiên làm việc.
### 3. Đặc tả xử lý ngoại lệ (Edge Cases)
#### 3.1. Người dùng nhập sai mật khẩu quá 5 lần
- **FR2.01**: Hệ thống lưu trữ và đếm số lần đăng nhập thất bại liên tiếp của một tài khoản.
- **FR2.02**: Khi số lần sai đạt mốc 5 lần, hệ thống tự động khóa tạm thời tính năng đăng nhập của tài khoản đó trong vòng 30 phút.
- **FR2.03**: Gửi email cảnh báo bảo mật tới địa chỉ email đã đăng ký của người dùng, kèm theo hướng dẫn đặt lại mật khẩu hoặc mở khóa.
- **FR2.04**: Hiển thị thông báo lỗi trên giao diện người dùng: "Tài khoản của bạn đã bị khóa tạm thời do nhập sai mật khẩu quá 5 lần. Vui lòng thử lại sau 30 phút hoặc kiểm tra email để biết thêm chi tiết."
#### 3.2. Token JWT hết hạn (expired) trong lúc phiên làm việc đang diễn ra
- **FR3.01**: Khi Access Token hết hạn, bất kỳ API request nào từ phía client cũng sẽ bị server từ chối với mã HTTP Status `401 Unauthorized`.
- **FR3.02**: Ứng dụng Client (Frontend) phải bắt được lỗi `401` này và tự động (ngầm) gửi request chứa Refresh Token đến endpoint `/api/auth/refresh-token` để xin cấp lại Access Token mới.
- **FR3.03**: Nếu Refresh Token hợp lệ, hệ thống trả về Access Token mới và các request đang dang dở của người dùng sẽ được tự động thực thi tiếp, không làm gián đoạn trải nghiệm người dùng (Silent Refresh).
- **FR3.04**: Nếu Refresh Token cũng đã hết hạn hoặc không hợp lệ, hệ thống buộc người dùng đăng xuất, xóa toàn bộ token lưu trữ dưới client và chuyển hướng về trang Đăng nhập kèm thông báo: "Phiên làm việc đã hết hạn. Vui lòng đăng nhập lại để tiếp tục."
#### 3.3. Tài khoản người dùng ở trạng thái khóa (Inactive) nhưng cố tình đăng nhập
- **FR4.01**: Ngay cả khi người dùng cung cấp đúng email và mật khẩu, hệ thống phải tiến hành kiểm tra trạng thái (Status) của tài khoản trong Database trước khi cấp Token.
- **FR4.02**: Nếu trạng thái là `Inactive` (hoặc `Locked`, `Banned`), hệ thống từ chối cấp phát JWT token.
- **FR4.03**: Hệ thống ghi log (Auditing) lại nỗ lực đăng nhập này để phục vụ công tác giám sát bảo mật.
- **FR4.04**: Trả về thông báo lỗi cụ thể trên màn hình: "Tài khoản của bạn hiện đang bị khóa hoặc chưa được kích hoạt. Vui lòng liên hệ bộ phận hỗ trợ khách hàng để được giải đáp."
### 4. Yêu cầu phi chức năng (Non-Functional Requirements)
- **Bảo mật**: Mật khẩu phải được băm (hashing) trước khi lưu trữ bằng các thuật toán mạnh (ví dụ: Bcrypt/Argon2). Refresh Token nên được lưu an toàn với HttpOnly Cookie.
- **Hiệu năng**: Quá trình kiểm tra thông tin và cấp phát JWT token phải hoàn thành dưới 500ms để đảm bảo trải nghiệm mượt mà.
```
