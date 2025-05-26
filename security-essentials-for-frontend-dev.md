# 📘 Security Essentials for Frontend Developers

## 1. Security Fundamentals (CIA + Non-repudiation)

- **Confidentiality (Bảo mật)**: Biết cách bảo vệ dữ liệu người dùng (email, token, session).
- **Integrity (Toàn vẹn)**: Dữ liệu hiển thị không bị giả mạo (ví dụ: không render HTML do user nhập).
- **Availability (Sẵn có)**: Ứng dụng không bị crash do lỗi input hoặc tấn công cơ bản.
- **Non-repudiation (Không thể chối bỏ)**: Biết cách kiểm tra log hoặc trace hành vi người dùng từ phía client.

## 2. Network & Protocols

- Hiểu rõ **HTTP**/**HTTPS**, biết sử dụng HTTPS ở mọi request.
- Biết đọc và xử lý **status code**: 200, 401, 403, 404, 500,...
- Biết cơ bản về **WebSocket**, nếu làm việc với ứng dụng real-time.
- Biết về **CORS**, nguyên nhân và cách khắc phục khi call API từ frontend.
- Hiểu sơ lược về **TCP/UDP** để giao tiếp với backend hiệu quả hơn (không cần chuyên sâu).

## 3. Application Security

### Các vấn đề thường gặp:

- **XSS (Cross-site Scripting)**: Không được render dữ liệu chưa được kiểm soát từ user.
- **CSRF (Cross-site Request Forgery)**: Hiểu và biết dùng CSRF token nếu app dùng cookie-based session.
- **Insecure Storage**: Không lưu thông tin nhạy cảm như token vào `localStorage` nếu có lựa chọn khác.

### Giải pháp cần nắm:

- Escape dữ liệu người dùng khi render:
```bash
const escapeHTML = (str) => str.replace(/</g, "&lt;").replace(/>/g, "&gt;");
Ưu tiên sử dụng HttpOnly Cookies thay vì lưu token ở localStorage.
```

Sử dụng Content-Security-Policy (CSP) để giảm thiểu nguy cơ XSS.

Không log thông tin nhạy cảm (token, email) trên trình duyệt.

## 4. Database Security
Không trực tiếp thao tác với database, nhưng cần hiểu:
- Dữ liệu nào được phép hiển thị ra UI?
- Tránh lộ thông tin quản trị, nội bộ, hay dữ liệu nhạy cảm.
- Giao tiếp với backend nên có xác thực rõ ràng (token, session).

## 5. Identity and Access Management (IAM)

Biết sử dụng và xác thực qua:

- JWT (JSON Web Token)
- OAuth2 (Google, Facebook login...)
- Session & Cookies

Hiểu khái niệm:

- RBAC (Role-based Access Control) ở frontend
- Phân quyền giao diện người dùng: ẩn/hiện chức năng theo vai trò người dùng

```bash
// Ví dụ phân quyền giao diện
if (user.role !== 'admin') {
  return <p>Bạn không có quyền truy cập chức năng này.</p>;
}
```

## 6. OWASP Top Ten (2021)

Các lỗi frontend developer cần quan tâm:

- A01: Broken Access Control – Kiểm tra quyền ở cả UI và backend.
- A03: Injection (XSS) – Không render HTML chưa được kiểm tra.
- A05: Security Misconfiguration – Thiết lập bảo mật đúng khi build frontend (CSP, headers...).
- A07: Identification and Authentication Failures – Biết kiểm soát token, session, timeout...
