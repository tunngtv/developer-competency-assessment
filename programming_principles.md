
# Nguyên tắc lập trình cơ bản cho Frontend Developer

## 1. DRY - Don't Repeat Yourself

**Định nghĩa:** Không lặp lại cùng một đoạn logic nhiều lần. Thay vào đó, trừu tượng hóa thành hàm, module, component tái sử dụng.

**Ví dụ sai:**
```js
function showUserProfile(user) {
  console.log(user.name);
  console.log(user.age);
}

function showAdminProfile(admin) {
  console.log(admin.name);
  console.log(admin.age);
}
```

**Cải tiến với DRY:**
```js
function showProfile(person) {
  console.log(person.name);
  console.log(person.age);
}
```

## 2. Single Responsibility Principle (SRP)

**Định nghĩa:** Mỗi module, class, hàm chỉ nên có _một lý do_ để thay đổi — tức là chỉ đảm nhiệm _một chức năng chính_.

**Ví dụ sai:**
```js
function saveUser(user) {
  validateUser(user);
  database.save(user);
  sendWelcomeEmail(user);
}
```

**Cải tiến với SRP:**
```js
function saveUser(user) {
  if (!validateUser(user)) return;
  database.save(user);
}

function sendWelcome(user) {
  sendEmail(user.email, "Welcome!");
}
```

## 3. Document Your Code

**Định nghĩa:** Viết chú thích, tài liệu rõ ràng để người khác (và chính bạn trong tương lai) dễ hiểu.

**Ví dụ:** Dùng JSDoc để mô tả hàm.

```js
/**
 * Tính tổng 2 số.
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
function sum(a, b) {
  return a + b;
}
```

---

## Tại sao quan trọng với Frontend Developer?
- Tăng khả năng bảo trì code base lớn.
- Dễ dàng làm việc nhóm (teamwork).
- Hạn chế bug do trùng lặp hoặc hiểu sai chức năng.
- Tạo tiền đề tốt để viết test, refactor và mở rộng.
