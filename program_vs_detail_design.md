# Thiết kế Program và Detail Design cho Frontend Developer

## 1. Program Design (Thiết kế chương trình)

Là giai đoạn thiết kế tổng quan của toàn bộ hệ thống hoặc module phần mềm.

### Mục tiêu:

- Xác định kiến trúc tổng thể (React, Vue, Angular...)
- Phân chia module hoặc component chính
- Định nghĩa luồng xử lý tổng quan
- Chọn pattern phù hợp (MVC, MVVM, Layered, v.v.)

### Ví dụ:

```text
App
├── AuthProvider (Quản lý đăng nhập)
│   ├── LoginPage
│   └── RegisterPage
├── Dashboard
│   ├── Profile
│   └── Settings
└── API Service Layer (axios setup)
```

---

## 2. Detail Design (Thiết kế chi tiết)

Là thiết kế chi tiết các module/component đã xác định ở bước Program Design.

### Mục tiêu:

- Thiết kế hàm, biến, class cụ thể
- Tên hàm và biến rõ ràng, dễ hiểu
- Xử lý lỗi và bất đồng bộ (async/await)
- Thiết kế UI logic, validation form

### Ví dụ: LoginPage component với React

```jsx
import { useState } from "react";
import { loginAPI } from "./api";

function LoginPage() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [error, setError] = useState("");

  async function handleLogin(e) {
    e.preventDefault();
    try {
      const token = await loginAPI({ email, password });
      localStorage.setItem("token", token);
      // redirect...
    } catch (err) {
      setError("Login failed");
    }
  }

  return (
    <form onSubmit={handleLogin}>
      <input value={email} onChange={(e) => setEmail(e.target.value)} />
      <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      {error && <div>{error}</div>}
      <button type="submit">Login</button>
    </form>
  );
}
```

---

## So sánh

| Yếu tố   | Program Design                      | Detail Design                                   |
| -------- | ----------------------------------- | ----------------------------------------------- |
| Mức độ   | Tổng thể (high-level)               | Cụ thể (low-level)                              |
| Mục tiêu | Phân chia module, flow logic        | Cài đặt cụ thể, xử lý logic chi tiết            |
| Dành cho | Người thiết kế hệ thống hoặc leader | Developer triển khai                            |
| Ví dụ    | React App cấu trúc nhiều page       | Chi tiết xử lý đăng nhập, API call, UI feedback |
