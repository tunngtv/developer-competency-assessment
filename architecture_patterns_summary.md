# 🧱 Các Mô Hình Kiến Trúc Phần Mềm Phổ Biến

---

## 1. Client-Server Pattern

### 💡 Lý thuyết

- Hệ thống được chia thành 2 phần:
  - **Client**: Giao diện người dùng, gửi yêu cầu.
  - **Server**: Xử lý logic, lưu trữ và phản hồi dữ liệu.
- Giao tiếp thông qua mạng (HTTP, WebSocket...).

### ✅ Ưu điểm

- Phân tách rõ ràng giữa giao diện và xử lý dữ liệu.
- Dễ mở rộng nhiều client (trình duyệt, mobile...).

### ⚠️ Nhược điểm

- Phụ thuộc vào kết nối mạng.
- Server dễ bị quá tải nếu client nhiều.

### 🧪 Ví dụ (JavaScript: Client → Server)

```javascript
// Client (Browser)
fetch("/api/users")
  .then((res) => res.json())
  .then((data) => console.log(data));
```

```javascript
// Server (Node.js + Express)
app.get("/api/users", (req, res) => {
  res.json([{ id: 1, name: "Alice" }]);
});
```

---

## 2. MVC (Model-View-Controller) Pattern

### 💡 Lý thuyết

- **Model**: Quản lý dữ liệu & logic nghiệp vụ.
- **View**: Giao diện người dùng.
- **Controller**: Nhận input từ user và điều phối.

### ✅ Ưu điểm

- Dễ tổ chức mã, tách biệt vai trò rõ ràng.
- Dễ bảo trì và mở rộng.

### 🧪 Ví dụ (JavaScript - Express + EJS)

```javascript
// Controller
app.get("/users", (req, res) => {
  const users = getUserList(); // Model
  res.render("users", { users }); // View
});
```

---

## 3. MVVM (Model-View-ViewModel)

### 💡 Lý thuyết

- **Model**: Quản lý dữ liệu và trạng thái.
- **ViewModel**: Logic kết nối giữa View và Model.
- **View**: Giao diện, tự động phản ứng với thay đổi của ViewModel (data-binding).

### ✅ Ưu điểm

- Dễ test (ViewModel tách khỏi View).
- Thích hợp cho UI phức tạp có binding động.

### 🧪 Ví dụ (JavaScript - Vue.js)

```javascript
<template>
  <input v-model="username" />
  <p>Hello, {{ username }}</p>
</template>

<script>
export default {
  data() {
    return { username: "Alice" };
  }
};
</script>
```

---

## 4. Layered Pattern (Kiến trúc phân lớp)

### 💡 Lý thuyết

- Hệ thống chia thành các lớp (layer) chức năng:
  - Presentation (Giao diện)
  - Application / Service (Logic nghiệp vụ)
  - Domain / Business (Quy tắc xử lý)
  - Data / Persistence (Lưu trữ)

### ✅ Ưu điểm

- Dễ tổ chức và bảo trì mã nguồn.
- Có thể thay đổi từng lớp mà không ảnh hưởng lớp khác.

### 🧪 Ví dụ (Giả lập kiến trúc đơn giản)

```javascript
// data.js (Data Layer)
const users = [{ id: 1, name: "Alice" }];
export function getUsers() {
  return users;
}

// service.js (Business Logic Layer)
import { getUsers } from "./data.js";
export function getUserNames() {
  return getUsers().map((u) => u.name);
}

// controller.js (Application Layer)
import { getUserNames } from "./service.js";
console.log(getUserNames()); // Output: ["Alice"]
```

---

## 📊 So sánh nhanh

| Pattern       | Vai trò chính                   | Ưu điểm               | Nhược điểm                    |
| ------------- | ------------------------------- | --------------------- | ----------------------------- |
| Client-Server | Phân chia UI & xử lý            | Dễ mở rộng, phổ biến  | Phụ thuộc mạng                |
| MVC           | Phân tách model-view-controller | Quản lý code rõ ràng  | View & Controller đôi khi rối |
| MVVM          | ViewModel làm trung gian        | Dễ test, binding mạnh | Phức tạp hơn khi debug        |
| Layered       | Tách theo tầng chức năng        | Linh hoạt, dễ bảo trì | Có thể dư thừa nếu app nhỏ    |

---

> 📌 Gợi ý: Trong buổi đánh giá, bạn nên:
>
> - Nắm mô hình nào dùng cho tình huống nào.
> - Giải thích flow hoạt động.
> - Có ví dụ nhỏ thể hiện sự hiểu rõ vai trò từng phần.
