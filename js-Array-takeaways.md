# JavaScript — Array Utils Functions (map / filter / find / reduce / some / every / sort / push / pop / shift / unshift)

> Nguồn nội dung: transcript video “JavaScript Array utils function”.  
> Lưu ý sửa tên hàm đúng chuẩn JS (trong transcript có chỗ đọc/ghi nhầm):
> - `file` → `find`
> - `short` → `sort`
> - `xăm` → `some`

---

## 1) `map()` — Biến đổi mảng (1 phần tử → 1 phần tử mới)

### Ý nghĩa
- Tạo **mảng mới** bằng cách áp dụng một hàm lên **từng phần tử** của mảng gốc.
- Mảng mới có **cùng độ dài** với mảng gốc.
- **Không làm thay đổi mảng gốc** (trừ trường hợp phần tử là object và mình sửa trực tiếp object đó).

### Cú pháp
```js
const newArr = arr.map((item, index, array) => {
  return /* giá trị mới */;
});
```

### Ví dụ 1 — Nhân đôi mảng số
```js
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(n => n * 2);

console.log(doubled); // [2, 4, 6, 8, 10]
console.log(numbers); // [1, 2, 3, 4, 5] (không đổi)
```

### Ví dụ 2 — Map nâng cao: tạo object từ mảng tên (dùng index)
```js
const names = ["An", "Binh", "Cuong"];

const studentList = names.map((name, index) => ({
  id: index + 1,
  name,
  code: `SV00${index + 1}`,
}));

console.log(studentList);
/*
[
  { id: 1, name: "An",    code: "SV001" },
  { id: 2, name: "Binh",  code: "SV002" },
  { id: 3, name: "Cuong", code: "SV003" }
]
*/
```

---

## 2) `filter()` — Lọc mảng theo điều kiện

### Ý nghĩa
- Tạo **mảng mới** chỉ gồm các phần tử **thỏa mãn điều kiện** trong callback.
- **Không làm thay đổi mảng gốc**.

### Cú pháp
```js
const filtered = arr.filter((item, index, array) => {
  return /* điều kiện true/false */;
});
```

### Ví dụ 1 — Lọc số chẵn
```js
const numbers = [1,2,3,4,5,6,7,8,9,10];
const evens = numbers.filter(n => n % 2 === 0);

console.log(evens);   // [2,4,6,8,10]
console.log(numbers); // mảng gốc không đổi
```

### Ví dụ 2 — Lọc sản phẩm theo điều kiện (1 điều kiện / nhiều điều kiện)
```js
const products = [
  { name: "iPhone",  price: 35, category: "phone",  inStock: true  },
  { name: "S24",     price: 30, category: "phone",  inStock: false },
  { name: "MacBook", price: 50, category: "laptop", inStock: true  },
  { name: "iPad",    price: 25, category: "tablet", inStock: true  },
  { name: "Asus",    price: 28, category: "laptop", inStock: true  },
];

// 1) sản phẩm còn hàng
const available = products.filter(p => p.inStock);

// 2) sản phẩm giá < 30
const under30 = products.filter(p => p.price < 30);

// 3) điện thoại còn hàng (kết hợp nhiều điều kiện)
const phoneInStock = products.filter(p => p.category === "phone" && p.inStock);

console.log(available);
console.log(under30);
console.log(phoneInStock);
```

---

## 3) `find()` — Tìm phần tử đầu tiên thỏa điều kiện

### Ý nghĩa
- Trả về **phần tử đầu tiên** thỏa điều kiện.
- Nếu không tìm thấy → `undefined`.
- **Dừng ngay** khi gặp phần tử đầu tiên thỏa mãn (tốt cho performance).

### Cú pháp
```js
const found = arr.find((item, index, array) => {
  return /* điều kiện true/false */;
});
```

### Ví dụ 1 — Find trên mảng số
```js
const numbers = [1, 3, 5, 8, 9];

console.log(numbers.find(n => n % 2 === 0)); // 8 (số chẵn đầu tiên)
console.log(numbers.find(n => n > 6));       // 8
console.log(numbers.find(n => n < 0));       // undefined
```

### Ví dụ 2 — Find trên mảng user
```js
const users = [
  { id: 1, name: "An",   role: "admin", active: true  },
  { id: 2, name: "Dung", role: "admin", active: false },
  { id: 3, name: "Ha",   role: "user",  active: true  },
];

console.log(users.find(u => u.id === 2));          // user id=2
console.log(users.find(u => u.role === "admin"));  // An (admin đầu tiên)
console.log(users.find(u => !u.active));           // Dung (không active)
```

> Ghi nhớ nhanh:
> - `filter()` trả về **mảng**
> - `find()` trả về **1 phần tử** (hoặc `undefined`)

---

## 4) `reduce()` — Tích lũy mảng thành 1 giá trị

### Ý nghĩa
- Duyệt qua mảng và **tích lũy** thành **một giá trị duy nhất**: số, chuỗi, object...
- Có 2 tham số quan trọng:
  - `accumulator (acc)`: giá trị tích lũy
  - `current (cur)`: phần tử hiện tại

### Cú pháp
```js
const result = arr.reduce((acc, cur, index, array) => {
  return /* giá trị acc mới */;
}, initialValue);
```

### Ví dụ 1 — Tính tổng mảng số
```js
const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce((acc, cur) => acc + cur, 0);
console.log(sum); // 15
```

### Ví dụ 2 — Tính tổng tiền giỏ hàng (price * quantity)
```js
const cart = [
  { name: "A", price: 10, quantity: 1 },
  { name: "B", price: 20, quantity: 2 },
  { name: "C", price: 15, quantity: 1 },
];

const totalMoney = cart.reduce((total, item) => {
  return total + item.price * item.quantity;
}, 0);

console.log(totalMoney);
```

### Ví dụ 3 — Tính tổng số lượng sản phẩm trong giỏ
```js
const totalQty = cart.reduce((acc, item) => acc + item.quantity, 0);
console.log(totalQty);
```

---

## 5) `some()` — Có ít nhất 1 phần tử thỏa điều kiện?

### Ý nghĩa
- Trả về `true` nếu **có ít nhất một** phần tử thỏa điều kiện.
- Trả về `false` nếu **không có** phần tử nào thỏa điều kiện.
- **Dừng sớm** ngay khi tìm thấy phần tử thỏa mãn.

### Cú pháp
```js
const ok = arr.some((item, index, array) => {
  return /* điều kiện true/false */;
});
```

### Ví dụ
```js
const numbers = [1, 3, 5, 7, 8, 9];

console.log(numbers.some(n => n % 2 === 0)); // true (vì có 8)
console.log(numbers.some(n => n > 10));      // false
```

---

## 6) `every()` — Tất cả phần tử đều thỏa điều kiện?

### Ý nghĩa
- Trả về `true` nếu **tất cả** phần tử thỏa điều kiện.
- Trả về `false` nếu **chỉ cần 1** phần tử không thỏa.
- **Dừng sớm** ngay khi gặp phần tử không thỏa mãn.

### Cú pháp
```js
const ok = arr.every((item, index, array) => {
  return /* điều kiện true/false */;
});
```

### Ví dụ 1 — Kiểm tra tất cả là số chẵn
```js
const numbers = [2, 4, 6, 8, 10];

console.log(numbers.every(n => n % 2 === 0)); // true
console.log(numbers.every(n => n > 5));       // false
console.log(numbers.every(n => n > 0));       // true
```

### Ví dụ 2 — Kiểm tra giỏ hàng có đủ tồn kho không
```js
const cart = [
  { name: "A", inStock: 5, quantity: 1 },
  { name: "B", inStock: 2, quantity: 2 },
  { name: "C", inStock: 1, quantity: 2 },
];

const canCheckout = cart.every(item => item.inStock >= item.quantity);
console.log(canCheckout); // false (vì C không đủ)
```

---

## 7) `sort()` — Sắp xếp mảng (⚠️ làm thay đổi mảng gốc)

### Ý nghĩa
- Sắp xếp phần tử trong mảng.
- Mặc định JS sort theo **alphabet (chuỗi)** → dễ gây hiểu lầm khi sort số.
- ⚠️ `sort()` **thay đổi trực tiếp mảng gốc** (mutate).

### Ví dụ 1 — Sort chuỗi (alphabet)
```js
const fruits = ["banana", "apple", "orange", "grape"];
fruits.sort();
console.log(fruits); // ["apple", "banana", "grape", "orange"]
```

### Ví dụ 2 — Bẫy khi sort số (mặc định sort theo chuỗi)
```js
const nums = [15, 40, 25, 1000, 1];
nums.sort();
console.log(nums); // [1, 1000, 15, 25, 40]
```

### Sort số đúng cách: compare function
- Tăng dần: `(a, b) => a - b`
- Giảm dần: `(a, b) => b - a`

```js
const nums = [15, 40, 25, 1000, 1];

nums.sort((a, b) => a - b);
console.log(nums); // [1, 15, 25, 40, 1000]

nums.sort((a, b) => b - a);
console.log(nums); // [1000, 40, 25, 15, 1]
```

#### Quy tắc compare function
- Trả về **số âm** → `a` đứng trước `b`
- Trả về **0** → giữ nguyên
- Trả về **số dương** → `b` đứng trước `a`

---

## 8) `push()` — Thêm phần tử vào cuối (⚠️ đổi mảng gốc)

### Ý nghĩa
- Thêm **1 hoặc nhiều** phần tử vào **cuối mảng**.
- ⚠️ Làm thay đổi mảng gốc.
- Trả về **độ dài mới** của mảng.

```js
const fruits = ["apple", "banana"];

const newLen = fruits.push("orange", "grape");
console.log(newLen); // 4
console.log(fruits); // ["apple","banana","orange","grape"]
```

---

## 9) `pop()` — Xóa phần tử cuối và trả về nó (⚠️ đổi mảng gốc)

### Ý nghĩa
- Xóa phần tử **cuối mảng** và **trả về** phần tử đó.
- Nếu mảng rỗng → trả về `undefined`.

```js
const fruits = ["apple", "banana", "grape"];

const last = fruits.pop();
console.log(last);   // "grape"
console.log(fruits); // ["apple","banana"]

const empty = [];
console.log(empty.pop()); // undefined
console.log(empty);       // []
```

---

## 10) `shift()` — Xóa phần tử đầu và trả về nó (⚠️ đổi mảng gốc)

### Ý nghĩa
- Xóa phần tử **đầu mảng** và **trả về** phần tử đó.
- Nếu mảng rỗng → `undefined`.

```js
const fruits = ["apple", "banana", "orange"];

const first = fruits.shift();
console.log(first);  // "apple"
console.log(fruits); // ["banana","orange"]

const empty = [];
console.log(empty.shift()); // undefined
console.log(empty);         // []
```

---

## 11) `unshift()` — Thêm phần tử vào đầu (⚠️ đổi mảng gốc)

### Ý nghĩa
- Thêm **1 hoặc nhiều** phần tử vào **đầu mảng**.
- ⚠️ Làm thay đổi mảng gốc.
- Trả về **độ dài mới** của mảng.

```js
const fruits = ["banana", "orange"];

const newLen = fruits.unshift("apple", "grape");
console.log(newLen); // 4
console.log(fruits); // ["apple","grape","banana","orange"]
```

---

## 12) Cheat Sheet

- `map()`   : biến đổi → **mảng mới** (cùng độ dài)
- `filter()`: lọc      → **mảng mới** (có thể ngắn hơn)
- `find()`  : tìm 1 cái → **phần tử / undefined** (dừng sớm)
- `reduce()`: gom      → **1 giá trị** (sum/obj/string…)
- `some()`  : có ít nhất 1? → **true/false** (dừng sớm)
- `every()` : tất cả đều đúng? → **true/false** (dừng sớm)
- `sort()`  : sắp xếp → ⚠️ **đổi mảng gốc**, số cần compare
- `push/pop/shift/unshift`: thêm/xóa đầu-cuối → ⚠️ **đổi mảng gốc**
