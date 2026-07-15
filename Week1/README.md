# Week 1 - Java Core & Linux Fundamentals

## Giới thiệu

Trong tuần đầu tiên của chương trình thực tập, mục tiêu là củng cố kiến thức nền tảng về Java Core và làm quen với môi trường Linux. Đây là hai kỹ năng quan trọng đối với lập trình viên Backend vì hầu hết các ứng dụng Java đều được phát triển dựa trên các nguyên lý hướng đối tượng và triển khai trên hệ điều hành Linux.

Báo cáo này tổng hợp các kiến thức lý thuyết đã tìm hiểu trong tuần, bao gồm Java Core, Collection Framework, Exception Handling, Linux Fundamentals và các khái niệm cơ bản liên quan đến hệ điều hành Linux.

---

# I. Java Core

## 1. Object-Oriented Programming (OOP)

### 1.1 OOP là gì?

Object-Oriented Programming (OOP) là phương pháp lập trình tổ chức chương trình thành các đối tượng (Object). Mỗi đối tượng chứa dữ liệu (Attributes) và các hành vi (Methods). OOP giúp tăng khả năng tái sử dụng, mở rộng và bảo trì phần mềm.

### 1.2 Bốn tính chất của OOP

#### Encapsulation (Đóng gói)

Encapsulation là kỹ thuật che giấu dữ liệu bên trong đối tượng và chỉ cho phép truy cập thông qua các phương thức được cung cấp. Điều này giúp bảo vệ dữ liệu và hạn chế việc thay đổi trạng thái của đối tượng từ bên ngoài.

**Ưu điểm**

- Bảo vệ dữ liệu.
- Giảm sự phụ thuộc giữa các lớp.
- Dễ bảo trì và mở rộng.

#### Inheritance (Kế thừa)

Inheritance cho phép một lớp kế thừa các thuộc tính và phương thức từ lớp khác. Điều này giúp tái sử dụng mã nguồn và giảm việc viết lại các chức năng giống nhau.

**Ưu điểm**

- Tái sử dụng mã nguồn.
- Dễ mở rộng hệ thống.
- Xây dựng mối quan hệ giữa các đối tượng.

#### Polymorphism (Đa hình)

Polymorphism cho phép nhiều đối tượng khác nhau thực hiện cùng một hành động theo các cách khác nhau. Trong Java, đa hình được thực hiện thông qua Method Overloading và Method Overriding.

**Ưu điểm**

- Tăng tính linh hoạt.
- Dễ mở rộng chức năng.
- Giảm phụ thuộc vào kiểu dữ liệu cụ thể.

#### Abstraction (Trừu tượng)

Abstraction là quá trình chỉ hiển thị những thông tin cần thiết và che giấu các chi tiết triển khai bên trong. Trong Java, tính trừu tượng được thực hiện thông qua Abstract Class và Interface.

**Ưu điểm**

- Giảm độ phức tạp của hệ thống.
- Tăng khả năng mở rộng.
- Dễ thay đổi cách triển khai mà không ảnh hưởng đến bên sử dụng.

---

## 2. SOLID Principles

SOLID là tập hợp năm nguyên lý thiết kế hướng đối tượng giúp xây dựng phần mềm dễ bảo trì, dễ mở rộng và dễ kiểm thử.

### Single Responsibility Principle (SRP)

Một lớp chỉ nên có một trách nhiệm và chỉ có một lý do để thay đổi.

**Ý nghĩa**

- Giảm sự phụ thuộc giữa các chức năng.
- Dễ kiểm thử.
- Dễ bảo trì.

### Open/Closed Principle (OCP)

Một lớp nên mở để mở rộng nhưng đóng để chỉnh sửa. Khi cần bổ sung chức năng mới nên mở rộng thay vì sửa trực tiếp mã nguồn hiện có.

**Ý nghĩa**

- Hạn chế phát sinh lỗi.
- Dễ mở rộng hệ thống.

### Liskov Substitution Principle (LSP)

Lớp con phải có thể thay thế lớp cha mà không làm thay đổi hành vi của chương trình.

**Ý nghĩa**

- Đảm bảo tính kế thừa đúng đắn.
- Tránh các lỗi khi sử dụng đa hình.

### Interface Segregation Principle (ISP)

Không nên ép một lớp phải triển khai những phương thức mà nó không sử dụng. Thay vì một Interface lớn nên chia thành nhiều Interface nhỏ.

**Ý nghĩa**

- Giảm sự phụ thuộc.
- Dễ mở rộng.
- Tăng tính linh hoạt.

### Dependency Inversion Principle (DIP)

Các module cấp cao không nên phụ thuộc trực tiếp vào module cấp thấp mà nên phụ thuộc vào Abstraction.

**Ý nghĩa**

- Giảm sự phụ thuộc giữa các thành phần.
- Dễ thay thế implementation.
- Hỗ trợ Dependency Injection trong Spring Framework.

---

## 3. Interface, Abstract Class và Static

### 3.1 Interface

Interface là bản thiết kế mô tả các hành vi mà một lớp phải thực hiện. Interface không chứa trạng thái của đối tượng và chủ yếu dùng để định nghĩa các phương thức.

**Đặc điểm**

- Hỗ trợ đa kế thừa.
- Chỉ mô tả hành vi.
- Giúp giảm sự phụ thuộc giữa các module.

**Khi sử dụng**

- Thiết kế API.
- Strategy Pattern.
- Service Layer trong Spring Boot.

---

### 3.2 Abstract Class

Abstract Class là lớp không thể khởi tạo trực tiếp và được dùng làm lớp cha cho các lớp khác.

**Đặc điểm**

- Có thể chứa cả phương thức trừu tượng và phương thức đã triển khai.
- Có thể chứa thuộc tính và constructor.
- Chỉ hỗ trợ kế thừa đơn.

**Khi sử dụng**

- Các lớp có nhiều đặc điểm chung.
- Muốn chia sẻ logic giữa nhiều lớp con.

---

### 3.3 So sánh Interface và Abstract Class

| Interface | Abstract Class |
|------------|----------------|
| Mô tả hành vi | Mô tả hành vi và trạng thái |
| Không lưu trạng thái đối tượng | Có thể chứa thuộc tính |
| Hỗ trợ đa kế thừa | Chỉ kế thừa một lớp |
| Thích hợp để giảm phụ thuộc | Thích hợp để tái sử dụng mã nguồn |

---

### 3.4 Static

`static` là từ khóa dùng để khai báo thành viên thuộc về lớp thay vì thuộc về từng đối tượng.

Các thành phần có thể khai báo `static`:

- Static Variable
- Static Method
- Static Block
- Static Nested Class

**Ứng dụng**

- Lưu hằng số.
- Hàm tiện ích (Utility Methods).
- Bộ đếm số lượng đối tượng.
- Khởi tạo tài nguyên dùng chung.

---

## 4. Collections Framework

### 4.1 Collections Framework là gì?

Collections Framework là tập hợp các Interface và Class được Java cung cấp để lưu trữ, quản lý và xử lý dữ liệu theo nhiều cấu trúc khác nhau như List, Set, Queue và Map.

### 4.2 Các Collection phổ biến

#### List

Lưu trữ dữ liệu có thứ tự và cho phép phần tử trùng lặp.

Ví dụ:

- ArrayList
- LinkedList

#### Set

Lưu trữ dữ liệu không trùng lặp.

Ví dụ:

- HashSet
- TreeSet

#### Queue

Lưu trữ dữ liệu theo cơ chế FIFO.

Ví dụ:

- PriorityQueue
- LinkedList

#### Map

Lưu dữ liệu theo cặp Key - Value.

Ví dụ:

- HashMap
- TreeMap
- LinkedHashMap

### 4.3 Performance

| Collection | Đặc điểm |
|------------|----------|
| ArrayList | Truy cập nhanh, thêm cuối nhanh |
| LinkedList | Thêm/xóa giữa danh sách hiệu quả |
| HashMap | Tra cứu theo Key rất nhanh |
| HashSet | Kiểm tra tồn tại nhanh |
| TreeMap | Dữ liệu được sắp xếp theo Key |

### 4.4 Thread-safe Collections

Trong môi trường đa luồng, Collection thông thường không đảm bảo an toàn dữ liệu. Java cung cấp các Collection thread-safe như:

- Vector
- Hashtable
- ConcurrentHashMap
- CopyOnWriteArrayList
- ConcurrentLinkedQueue

Các Collection này sử dụng cơ chế đồng bộ hoặc thuật toán concurrent để giảm xung đột giữa các luồng.

---

## 5. Exception Handling

### 5.1 Exception là gì?

Exception là các sự kiện bất thường xảy ra trong quá trình thực thi chương trình làm gián đoạn luồng xử lý bình thường.

### 5.2 Phân loại Exception

#### Checked Exception

Được kiểm tra tại thời điểm biên dịch và bắt buộc phải xử lý.

Ví dụ:

- IOException
- SQLException

#### Unchecked Exception

Xảy ra trong quá trình chạy chương trình.

Ví dụ:

- NullPointerException
- ArithmeticException
- IndexOutOfBoundsException

#### Error

Lỗi nghiêm trọng của JVM, thường không thể xử lý bằng chương trình.

Ví dụ:

- OutOfMemoryError
- StackOverflowError

### 5.3 Các từ khóa

- `try`: Khối mã có thể phát sinh Exception.
- `catch`: Xử lý Exception.
- `finally`: Luôn được thực thi sau khi try/catch kết thúc.
- `throw`: Chủ động phát sinh Exception.
- `throws`: Khai báo Exception mà phương thức có thể phát sinh.

### 5.4 Best Practices

- Chỉ bắt những Exception cần thiết.
- Không sử dụng `catch (Exception e)` nếu không thực sự cần.
- Sử dụng Custom Exception để biểu diễn lỗi nghiệp vụ.
- Ghi log đầy đủ trước khi xử lý Exception.
- Sử dụng `try-with-resources` để tự động đóng tài nguyên.
- Trong Spring Boot nên sử dụng Global Exception Handler để xử lý lỗi tập trung.
