# Developer-competency-assessment-

# 🔍 Tổng Quan Các Phương Pháp Thiết Kế Phần Mềm

## 1. Object-Oriented Design (OOD)

### 💡 Lý thuyết

- Thiết kế dựa trên **class** và **object**.
- Mô hình hóa thực thể thế giới thực thành các đối tượng phần mềm.
- Dựa trên 4 nguyên lý chính:
  - **Encapsulation (Đóng gói)**
  - **Abstraction (Trừu tượng hóa)**
  - **Inheritance (Kế thừa)**
  - **Polymorphism (Đa hình)**

### ✅ Phù hợp khi:

- Ứng dụng có cấu trúc phức tạp, nhiều thực thể.
- Cần mở rộng, tái sử dụng code.

### 🧪 Ví dụ (JavaScript):

```javascript
class BankAccount {
  constructor(owner, balance = 0) {
    this.owner = owner;
    this.balance = balance;
  }

  deposit(amount) {
    this.balance += amount;
  }

  withdraw(amount) {
    if (amount > this.balance) {
      throw new Error("Insufficient funds");
    }
    this.balance -= amount;
  }

  getBalance() {
    return this.balance;
  }
}

const account = new BankAccount("Alice");
account.deposit(1000);
account.withdraw(200);
console.log(account.getBalance()); // 800
```

---

## 2. Function-Oriented Design (FOD)

### 💡 Lý thuyết

- Thiết kế dựa trên việc **phân tách các chức năng** thành các hàm nhỏ.
- Tập trung vào **luồng dữ liệu**, từng bước xử lý qua các hàm.
- Không dùng class/đối tượng.

### ✅ Phù hợp khi:

- Hệ thống thiên về xử lý dữ liệu hoặc tính toán.
- Cần dễ dàng kiểm thử từng chức năng riêng biệt.

### 🧪 Ví dụ (JavaScript):

```javascript
function createAccount(owner, balance = 0) {
  return { owner, balance };
}

function deposit(account, amount) {
  return { ...account, balance: account.balance + amount };
}

function withdraw(account, amount) {
  if (amount > account.balance) throw new Error("Insufficient funds");
  return { ...account, balance: account.balance - amount };
}

function getTotalBalance(accounts) {
  return accounts.reduce((total, acc) => total + acc.balance, 0);
}

const acc1 = createAccount("Alice", 1000);
const acc2 = deposit(createAccount("Bob", 500), 200);
console.log(getTotalBalance([acc1, acc2])); // 1700
```

---

## 3. Structured Design

### 💡 Lý thuyết

- Thiết kế theo kiểu **Top-down**: từ chức năng chính chia thành các module nhỏ hơn.
- Dựa trên nguyên lý của **Structured Programming**: sử dụng rõ ràng các cấu trúc điều khiển như `if`, `loop`, `function`.
- Không sử dụng hướng đối tượng, chủ yếu tập trung vào logic.

### ✅ Phù hợp khi:

- Bài toán xử lý có quy trình rõ ràng, tuần tự.
- Cần kiểm soát luồng xử lý chặt chẽ.

### 🧪 Ví dụ (JavaScript):

```javascript
function validateOrder(order) {
  return order.items.length > 0 && order.total > 0;
}

function calculateTotal(order) {
  return order.items.reduce((sum, item) => sum + item.price * item.quantity, 0);
}

function processOrder(order) {
  if (!validateOrder(order)) {
    throw new Error("Invalid order");
  }

  order.total = calculateTotal(order);
  // Thêm các bước xử lý tiếp theo như lưu DB, gửi email,...
  console.log("Order processed:", order);
}

const order = {
  items: [
    { name: "Laptop", price: 1000, quantity: 1 },
    { name: "Mouse", price: 50, quantity: 2 },
  ],
  total: 0,
};

processOrder(order);
// Output: Order processed: { items: [...], total: 1100 }
```

---

## 📌 So sánh nhanh

| Tiêu chí              | Object-Oriented Design    | Function-Oriented Design | Structured Design         |
| --------------------- | ------------------------- | ------------------------ | ------------------------- |
| Đơn vị thiết kế chính | Class, Object             | Function                 | Function, Module          |
| Tập trung             | Trạng thái + hành vi      | Chức năng xử lý          | Luồng xử lý theo cấu trúc |
| Tái sử dụng           | Rất cao                   | Trung bình               | Trung bình                |
| Độ phức tạp           | Cao, phù hợp hệ thống lớn | Vừa, dễ test             | Vừa, dễ hiểu              |
| Ngôn ngữ phù hợp      | JavaScript (ES6+), Java   | JavaScript, Python, Go   | JavaScript, C, Pascal     |

---

> 💬 **Gợi ý ôn tập**: Trong buổi đánh giá, bạn nên nắm vững:
>
> - Điểm mạnh và hạn chế của từng phương pháp.
> - Cách áp dụng linh hoạt trong dự án thực tế.
> - Viết code ví dụ đơn giản thể hiện rõ tư duy thiết kế tương ứng.
