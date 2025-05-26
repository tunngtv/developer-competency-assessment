# 🎨 Tổng Quan Về Các Design Patterns Cơ Bản

Design Patterns là các giải pháp đã được kiểm chứng cho những vấn đề phổ biến trong thiết kế phần mềm. Chúng giúp hệ thống dễ bảo trì, mở rộng và dễ hiểu hơn.

---

## 1. Creational Design Patterns (Tạo đối tượng)

### 🔹 Factory Method

- Cung cấp interface để tạo đối tượng, nhưng để các lớp con quyết định class nào sẽ được khởi tạo.

```javascript
class Dog {
  speak() {
    return "Woof";
  }
}

class Cat {
  speak() {
    return "Meow";
  }
}

function animalFactory(type) {
  if (type === "dog") return new Dog();
  if (type === "cat") return new Cat();
}
```

### 🔹 Abstract Factory

- Tạo ra các nhóm đối tượng liên quan mà không cần xác định lớp cụ thể.

```javascript
function createAnimalFactory(type) {
  return type === "wild" ? () => new Tiger() : () => new Cat();
}
```

### 🔹 Builder

- Tách việc xây dựng đối tượng phức tạp khỏi biểu diễn của nó.

```javascript
class BurgerBuilder {
  constructor() {
    this.ingredients = [];
  }
  addCheese() {
    this.ingredients.push("cheese");
    return this;
  }
  addLettuce() {
    this.ingredients.push("lettuce");
    return this;
  }
  build() {
    return this.ingredients;
  }
}

const burger = new BurgerBuilder().addCheese().addLettuce().build();
```

### 🔹 Prototype

- Tạo đối tượng mới bằng cách sao chép một đối tượng hiện có.

```javascript
const car = {
  wheels: 4,
  drive() {
    return "vroom";
  },
};
const myCar = Object.create(car);
```

### 🔹 Singleton

- Đảm bảo một class chỉ có duy nhất một instance.

```javascript
const Singleton = (function () {
  let instance;
  return {
    getInstance: function () {
      if (!instance) instance = { time: Date.now() };
      return instance;
    },
  };
})();
```

---

## 2. Structural Design Patterns (Cấu trúc đối tượng)

### 🔹 Adapter

- Chuyển interface của một class sang interface khác mà client mong muốn.

```javascript
class OldPrinter {
  print() {
    console.log("Old printer");
  }
}

class NewPrinter {
  constructor(oldPrinter) {
    this.oldPrinter = oldPrinter;
  }
  printDocument() {
    this.oldPrinter.print();
  }
}
```

### 🔹 Bridge

- Tách abstraction khỏi implementation.

```javascript
class Device {
  turnOn() {
    console.log("Device on");
  }
}

class Remote {
  constructor(device) {
    this.device = device;
  }
  power() {
    this.device.turnOn();
  }
}
```

### 🔹 Composite

- Dùng để xử lý các đối tượng dạng cây (tree structure).

```javascript
class Component {
  constructor(name) {
    this.name = name;
    this.children = [];
  }
  add(child) {
    this.children.push(child);
  }
}
```

### 🔹 Decorator

- Thêm chức năng cho đối tượng mà không thay đổi code gốc.

```javascript
function coffee() {
  return "coffee";
}
function withMilk(c) {
  return () => c() + " + milk";
}
const milkCoffee = withMilk(coffee);
```

### 🔹 Facade

- Cung cấp interface đơn giản cho hệ thống phức tạp.

```javascript
class Computer {
  boot() {
    return "Booting...";
  }
}

class Facade {
  constructor() {
    this.computer = new Computer();
  }
  start() {
    return this.computer.boot();
  }
}
```

### 🔹 Flyweight

- Dùng lại nhiều đối tượng nhỏ thay vì tạo mới.

```javascript
const flyweights = {};
function getChar(char) {
  if (!flyweights[char]) flyweights[char] = { char };
  return flyweights[char];
}
```

### 🔹 Proxy

- Đại diện cho đối tượng khác để kiểm soát truy cập.

```javascript
function createProxy(target) {
  return new Proxy(target, {
    get(obj, prop) {
      console.log("Accessing", prop);
      return obj[prop];
    },
  });
}
```

---

## 3. Behavioral Design Patterns (Hành vi đối tượng)

### 🔹 Chain of Responsibility

```javascript
class Handler {
  setNext(handler) {
    this.next = handler;
    return handler;
  }
  handle(req) {
    if (this.next) return this.next.handle(req);
    return null;
  }
}
```

### 🔹 Command

```javascript
class Light {
  turnOn() {
    console.log("Light On");
  }
}

class Command {
  constructor(receiver) {
    this.receiver = receiver;
  }
  execute() {
    this.receiver.turnOn();
  }
}
```

### 🔹 Iterator

```javascript
const iterator = [1, 2, 3][Symbol.iterator]();
console.log(iterator.next());
```

### 🔹 Memento

```javascript
class Editor {
  constructor() {
    this.content = "";
  }
  save() {
    return this.content;
  }
  restore(memento) {
    this.content = memento;
  }
}
```

### 🔹 Mediator

```javascript
class ChatRoom {
  showMessage(user, message) {
    console.log(`[${user}]: ${message}`);
  }
}
```

### 🔹 Observer

```javascript
class Subject {
  constructor() {
    this.observers = [];
  }
  subscribe(fn) {
    this.observers.push(fn);
  }
  notify(data) {
    this.observers.forEach((fn) => fn(data));
  }
}
```

### 🔹 State

```javascript
class State {
  handle() {
    console.log("Handling state...");
  }
}
```

### 🔹 Strategy

```javascript
function travel(strategy) {
  strategy();
}
travel(() => console.log("Traveling by car"));
```

### 🔹 Template Method

```javascript
class Meal {
  cook() {
    this.prepare();
    this.serve();
  }
}
```

### 🔹 Visitor

```javascript
function accept(visitor, node) {
  visitor.visit(node);
}
```

---

📘 Tham khảo thêm: [Refactoring Guru - Design Patterns](https://refactoring.guru/design-patterns)
