# **Lesson 03: Key takeaways**

## A. Review homework
1. Format Code: gõ đến đâu format đến đấy hoặc chọn "Format Document" là tính năng đặc biệt.
2. Thống nhất trình bày cho bài tập thực hành GIT theo trạng thái của các vùng(Working, Staging, Repository) theo từng câu lệnh.
## B. Nội dung chính của bài học
## I. Git(Undo actions & tạo branch)
### 1. Undo actions
**Có 3 loại Undo**:
> 1. Commit message
> 2. File staging -> working directory
> 3. File reposity -> working directory
---
#### 1. Commit message
> **Cú pháp**: `git commit --amend -m "message"`

> **Thực hành**:
- Mở Visual Studio.
- Mở thư mục pw-course ( đã khởi tạo `git init`) hoặc tạo thư mục mới khác thì sẽ khởi tạo `git init` lại.
- Tạo thư mục lesson03.
- Tạo file file1.txt và thực hành trên đó.
- Mở terminal ra. 
- Gõ lệnh: `git add file1.txt`
- Gõ lệnh: `git commit -m "message bi sai"`
- Gõ lệnh: `git log`
- Gõ lệnh: `git commit --amen -m "message da fix"`

#### 2. File staging -> working directory
> **Cú pháp**: `git restore --staged <file_name>`

> **Thực hành**:
- Tạo thêm các file: file2.txt, file3.txt, file4.txt.
- Gõ lệnh: `git add .` // thêm tất cả file vào vùng Staging.
- Gõ lệnh: `git status` //xem trạng thái các file.
- Gõ lệnh: `git restore --staged file3.txt` //chuyển file3 lại vùng Working.
- Gõ lệnh: `git status` //xem trạng thái lại của file3 đã về Working chưa.

#### 3. File reposity -> working directory ( còn gọi là uncommit)
> **Cú pháp**: `git reset HEAD~N` //N: số lượng commit

> **Ứng dụng**: khi commit nhầm

> **Lưu ý**: 
- Commit đầu tiên không thể bị reset
- Nếu muốn reset -> xóa thư mục .git đi rồi init lại
> **Thực hành**: 
- Tạo các file mới hoàn toàn vào vd: file1.txt, file2.txt,file3.txt.
- Lần lượt commit từng file :
- Gõ lệnh: `git add file1.txt` -> `git commit -m "commit file1.txt"`
- Gõ lệnh: `git add file2.txt` -> `git commit -m "commit file2.txt"`
- Gõ lệnh: `git add file3.txt` -> `git commit -m "commit file3.txt"`
- Gõ lệnh: `git status` //xem trạng thái các file.
- Gõ lệnh: `git log` //xem hiện trạng commit.
- Gõ lệnh: `git reset HEAD~N` //thực hành uncommit.
- Gõ lệnh: `git log` //xem hiện trạng commit giờ thế nào.
- Note: thực hành nhuần nhuyễn và xem trạng thái thay đổi của file sau mỗi cập nhật bài học.

__Tóm tắt lệnh phần học Undo này:__
```
> git commit --amend -m "new_comment"
> git restore --staged file_name
> git reset HEAD~N
``` 

### 2. Branching modes: tạo nhánh
```
Đẩy code lên(commit): git push origin ten_nhanh
Kéo code về máy: git pull origin ten_nhanh
```
#### 2.1. Khái niệm : Nhánh được sử dụng để tạo ra các phiên bản khác nhau của Code.

#### 2.2. Cú pháp

---

`git config global init.defaultBranch main` : đặt tên nhánh mặc định là main.
***(ở bài học 1 đã học cấu hình tên, email & nhánh main)***

 `git branch`: 
    >> 1. xem danh sách.
    >> 2. xem đang đứng nhánh nào.

 `git branch ten_nhanh`: tạo thêm nhánh mới( sao chép toàn bộ thư mục của main)

 `git checkout lesson-03`: chuyển sang nhánh lesson-03 (hiển thị terminal là : Switched to branch 'lesson-03')

 `git checkout -b <tên>`: vừa tạo vừa chuyển sang(hiển thị terminal là : Switched to branch 'lesson-03')

 `git branch -D lesson-03`: xóa branch lesson-03 đi

---

***__Lưu ý__: luôn luôn pull code về trước khi tạo nhánh mới***

#### 2.3. File .gitignore
**Ý nghĩa:**
- .gitignore là file dùng để nói với Git: “đừng theo dõi (track) những file này”.

- File khớp rule trong .gitignore sẽ không hiện để commit.

- .gitignore chỉ có tác dụng với file CHƯA bị track.

**Nội dung của file .gitignore:**

Cú pháp:  tenfile/
#### 2.3. VS CODE: xem thay đổi

## II. Javascript Basic
### 1. Conventions
Có 4 kiểu:
1. snake_case: chưa dùng

2. kebab-case: đặt tên file

3. camelCase: tên biến

4. PascalCase: tên class

### 2. Console.log: Formatted

```js
const name = "Ngoc";
console.log ("Toi la Ngoc");
console.log ('Toi la Ngoc');
console.log (`Toi la Ngoc`);
console.log (`Toi la ${name}`);
console.log ("Toi la "+ name);
console.log ("Toi la ", name);
```
>> Kết quả in ra: Toi la Ngoc

### 3.Object

**Ý nghĩa:** đối tượng, lưu trữ tập hợp các giá trị hoặc biến vào 1 hằng số

**Cú pháp khai báo:** 

`let/const <ten_object>= {<thuoc_tinh>: <gia_tri> ,}`

Ví dụ:
```JS
let student ={
name : "Ngoc",
role: "student",
age: `25`,
class:
{
name: "K101",
subject: "Fullstack Automation"   
}
}
//Có 2 cách để in ra giá trị của Đối tượng tên:
//cách 1:
console.log(student.name);
console.log(student.class.name);
//cách 2:
console.log(student["name"]);
console.log(student["class"]["name"]);

//Khi nào chọn cách 1 hoặc 2( tự tham khảo chatgpt)

>>Dùng cách 1 nếu key “đẹp” và cố định → code dễ đọc.
>>Dùng cách 2 khi:
>>key có ký tự đặc biệt / dấu cách,
>>key lấy từ biến (API trả về, loop, dynamic),
>>cần truy cập sâu kiểu obj[key1][key2].
```

### 4. Array (Mảng)

**Khái niệm:** Array dùng để lưu danh sách.

#### 4.1. Cú pháp khai báo mảng
const members = ["Thao", "Phuong", "Hien", "Hieu", "Uyen"];

#### 4.2 Ý quan trọng trong mảng

length = số lượng phần tử

`console.log(members.length);`


index bắt đầu từ 0 đến length - 1
Ví dụ: members[0] là phần tử đầu tiên.
```
console.log(members[0]); // "Thao"
console.log(members[4]); // "Uyen"`
```
### 5. Function (Hàm)

**Khái niệm:** Function là đoạn code được đặt tên để tái sử dụng, thực hiện 1 nhiệm vụ cụ thể.

#### 5.1. Khai báo hàm & gọi hàm
```
function sayHelloWorld() {
  console.log("Hello World");
}

sayHelloWorld();
```

**Lưu ý:** Chỉ khai báo function thì chưa chạy. Phải gọi hàm (tên hàm + ()) thì mới thực thi.

#### 5.2. Function có tham số (parameter)

**Mục đích:** làm hàm linh hoạt, truyền giá trị vào để hàm chạy theo yêu cầu.

Ví dụ: đếm từ 0 đến n rồi in “Hello World”
```
function countBeforeHello(n) {
  for (let i = 0; i <= n; i++) {
    console.log(i);
  }
  console.log("Hello World");
}

countBeforeHello(10);
```

#### 5.3. Function có return (trả về giá trị)
```
function sum(a, b) {
  const total = a + b;
  return total;
}
const result = sum(5, 6);
console.log(result);
```

>Lưu ý quan trọng về return:
 >>Gặp return là thoát khỏi function ngay, các dòng dưới sẽ không chạy nữa.

### 6. Bài thực hành cuối buổi: getMax(a, b)

Yêu cầu: nhận vào 2 số a, b và trả về số lớn hơn.

Gợi ý theo lớp (dễ hiểu, đúng kiến thức đã học):
```
function getMax(a, b) {
  if (a > b) {
    return a;
  }
  return b;
}
```