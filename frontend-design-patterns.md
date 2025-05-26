# Design Patterns cho Frontend Developer (Vue & React)

## 1. Component Pattern

**Mô tả**: Tái sử dụng UI bằng các components nhỏ, có thể kết hợp và tổ chức lại.

**Ví dụ**:

- React: Functional Components, Class Components
- Vue: Single File Components (SFCs)

**Lợi ích**: Tách biệt UI, tăng tính modular, dễ test.

---

## 2. Container / Presentational Pattern

**Mô tả**:

- _Container_: Quản lý state, logic, dữ liệu.
- _Presentational_: Chỉ tập trung vào UI, nhận props.

**Lợi ích**: Tách biệt logic và UI giúp code dễ bảo trì và test.

**Ví dụ React**:

```jsx
// Container Component
function UserContainer() {
  const [user, setUser] = React.useState(null);
  React.useEffect(() => {
    fetchUser().then(setUser);
  }, []);
  return <UserProfile user={user} />;
}

// Presentational Component
function UserProfile({ user }) {
  return <div>{user?.name}</div>;
}
```

---

## 3. Higher-Order Component (HOC)

**Mô tả**: Hàm nhận component và trả về component mới có thêm tính năng.

**Lợi ích**: Tái sử dụng logic, ví dụ authentication, logging.

**Ví dụ React**:

```jsx
function withLogger(WrappedComponent) {
  return function (props) {
    console.log("Rendering", WrappedComponent.name);
    return <WrappedComponent {...props} />;
  };
}
```

---

## 4. Render Props

**Mô tả**: Component nhận một function (render prop) để linh hoạt render UI.

**Lợi ích**: Tái sử dụng logic với UI khác nhau.

**Ví dụ React**:

```jsx
function MouseTracker({ render }) {
  const [pos, setPos] = React.useState({ x: 0, y: 0 });
  React.useEffect(() => {
    const handleMove = (e) => setPos({ x: e.clientX, y: e.clientY });
    window.addEventListener("mousemove", handleMove);
    return () => window.removeEventListener("mousemove", handleMove);
  }, []);
  return render(pos);
}

// Dùng:
<MouseTracker
  render={(pos) => (
    <p>
      Mouse at {pos.x}, {pos.y}
    </p>
  )}
/>;
```

---

## 5. Observer Pattern (Pub/Sub)

**Mô tả**: Quản lý sự kiện hoặc state thay đổi (event bus hoặc state management).

**Ví dụ**: Vue’s `watch`, React Context, Redux, hoặc EventEmitter.

**Lợi ích**: Giúp giao tiếp giữa components hoặc modules một cách rõ ràng.

---

## 6. Singleton Pattern

**Mô tả**: Đảm bảo chỉ có một instance của một đối tượng (ví dụ: global store, event bus).

**Ví dụ**: Vuex Store, React Context Provider.

**Lợi ích**: Quản lý trạng thái ứng dụng tập trung.

---

## 7. Module Pattern

**Mô tả**: Tổ chức code theo module riêng biệt (ES6 module, CommonJS).

**Lợi ích**: Code có cấu trúc, tái sử dụng được, tránh xung đột tên biến.

---

## 8. Strategy Pattern

**Mô tả**: Thay đổi hành vi hoặc thuật toán tại runtime bằng cách truyền strategy (hàm hoặc object).

**Ví dụ**: Trong React, truyền callback cho event handlers để thay đổi cách xử lý.

**Lợi ích**: Giúp code dễ mở rộng và tùy biến.

---

## Tổng kết ngắn gọn

| Pattern                  | Tầm quan trọng với Vue/React | Tại sao?                    |
| ------------------------ | ---------------------------- | --------------------------- |
| Component                | ⭐ Rất quan trọng            | Cơ sở xây dựng UI modular   |
| Container/Presentational | ⭐⭐ Quan trọng              | Tách biệt logic & UI        |
| HOC                      | ⭐⭐ Quan trọng              | Tái sử dụng logic           |
| Render Props             | ⭐⭐ Khá quan trọng          | Tính linh hoạt trong render |
| Observer                 | ⭐⭐ Quan trọng              | Quản lý event, state        |
| Singleton                | ⭐⭐ Quan trọng              | Quản lý state toàn cục      |
| Module                   | ⭐ Cơ bản                    | Tổ chức code                |
| Strategy                 | ⭐ Có thể dùng               | Thay đổi logic runtime      |
