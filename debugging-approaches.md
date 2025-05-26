# 🔍 Debugging Approaches for Frontend Developers

## 1. Brute Force Method

### Mô tả:
Involves reading the entire code base line-by-line or adding print/logging statements (`console.log`) at multiple places to trace execution.

### Ưu điểm:
- Dễ thực hiện
- Không cần công cụ nâng cao

### Nhược điểm:
- Tốn thời gian
- Dễ bỏ sót lỗi logic

### Ví dụ (JavaScript):
```js
function getUserName(user) {
  console.log("User object:", user);
  return user && user.name;
}
```

---

## 2. Backtracking

### Mô tả:
Bắt đầu từ vị trí nơi lỗi xảy ra và lần ngược lại logic hoặc luồng thực thi để tìm nguyên nhân.

### Ưu điểm:
- Tập trung vào điểm lỗi
- Hiệu quả nếu hiểu rõ logic chương trình

### Nhược điểm:
- Khó thực hiện nếu code phức tạp

### Ví dụ:
Khi nhận lỗi ở màn hình hiển thị, lần ngược lại:
1. Component rendering → 2. Props truyền vào → 3. API trả về → 4. Request setup → 5. Trigger action

---

## 3. Cause Elimination Method

### Mô tả:
Loại bỏ từng giả thuyết về nguyên nhân lỗi bằng cách tắt, đổi hoặc cô lập các đoạn mã hoặc tính năng.

### Ưu điểm:
- Hiệu quả trong môi trường phức tạp
- Tìm lỗi bằng cách loại trừ

### Nhược điểm:
- Có thể mất thời gian
- Cần biết cách cô lập đúng phần nghi ngờ

### Ví dụ:
- Vô hiệu hóa cache API để kiểm tra kết quả
- Bỏ CSS từng phần để xem lỗi layout còn xảy ra không
- Dùng mock data thay vì thật

---

## 4. Program Slicing

### Mô tả:
Chỉ tập trung vào một **đoạn nhỏ của chương trình** có liên quan đến lỗi (slicing), bỏ qua những phần không liên quan.

### Ưu điểm:
- Giảm nhiễu, tập trung hơn
- Hữu ích khi làm việc với project lớn

### Nhược điểm:
- Cần kỹ năng xác định phạm vi slice đúng

### Ví dụ:
Giả sử hàm `calculateTotalPrice(cart)` có lỗi, bạn chỉ test function đó độc lập với dữ liệu đơn giản, không cần toàn bộ app chạy.

```js
function calculateTotalPrice(cart) {
  return cart.reduce((total, item) => total + item.price * item.quantity, 0);
}

// Slice test
console.log(calculateTotalPrice([
  { price: 100, quantity: 2 },
  { price: 50, quantity: 1 }
])); // Expected output: 250
```

---

## 🎯 Kết luận

| Phương pháp           | Khi nào dùng                                     |
|------------------------|--------------------------------------------------|
| Brute Force           | Khi mới bắt đầu hoặc không rõ điểm lỗi           |
| Backtracking          | Khi biết lỗi xảy ra ở đâu và muốn truy ngược     |
| Cause Elimination     | Khi có nhiều khả năng nguyên nhân khác nhau      |
| Program Slicing       | Khi code lớn và bạn muốn cô lập phạm vi phân tích|

---

## 🔗 Tham khảo

- [Debugging Approaches - GeeksForGeeks](https://www.geeksforgeeks.org/debugging-approaches/)
- Chrome DevTools
- VSCode Debugger
- React/Vue DevTools
