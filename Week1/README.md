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

---

# II. Linux Fundamentals

## 1. Linux là gì?

Linux là một hệ điều hành mã nguồn mở được xây dựng dựa trên nhân (Kernel) Linux. Nhờ tính ổn định, bảo mật và hiệu năng cao, Linux được sử dụng rộng rãi trên máy chủ, hệ thống Cloud, Docker và các môi trường triển khai ứng dụng Backend.

Trong quá trình phát triển phần mềm, lập trình viên Backend thường làm việc trên môi trường Linux để chạy ứng dụng, quản lý tiến trình, kiểm tra log và triển khai hệ thống.

---

## 2. File System

Linux tổ chức dữ liệu theo dạng cây thư mục, bắt đầu từ thư mục gốc `/`. Mọi tệp và thư mục đều nằm trong cấu trúc này.

Một số thư mục quan trọng:

| Thư mục | Chức năng |
|---------|-----------|
| `/` | Thư mục gốc của hệ thống |
| `/home` | Thư mục người dùng |
| `/root` | Thư mục của tài khoản root |
| `/etc` | Tệp cấu hình hệ thống |
| `/bin` | Các lệnh cơ bản |
| `/usr` | Chương trình và thư viện |
| `/var` | Dữ liệu thay đổi thường xuyên như log |
| `/tmp` | Tệp tạm thời |

Linux sử dụng hai loại đường dẫn:

- **Absolute Path:** bắt đầu từ thư mục gốc `/`
- **Relative Path:** tính từ thư mục hiện tại

Các lệnh thường dùng:

- `pwd`: hiển thị thư mục hiện tại.
- `ls`: liệt kê file và thư mục.
- `cd`: chuyển thư mục.
- `mkdir`: tạo thư mục.
- `touch`: tạo file.
- `cp`: sao chép.
- `mv`: di chuyển hoặc đổi tên.
- `rm`: xóa file hoặc thư mục.

---

## 3. File Permissions

Linux sử dụng cơ chế phân quyền để kiểm soát quyền truy cập vào file và thư mục.

Mỗi file có ba nhóm quyền:

- User (Owner)
- Group
- Other

Ba loại quyền:

- **r (Read):** đọc.
- **w (Write):** ghi.
- **x (Execute):** thực thi.

Ví dụ:

```
-rwxr-xr--
```

Các lệnh thường dùng:

### chmod

Thay đổi quyền truy cập của file.

Ví dụ:

```bash
chmod 755 script.sh
```

### chown

Thay đổi chủ sở hữu của file hoặc thư mục.

Ví dụ:

```bash
chown user:group file.txt
```

### umask

Thiết lập quyền mặc định khi tạo file hoặc thư mục mới.

Ví dụ:

```bash
umask 022
```

---

## 4. Process Management

Process là một chương trình đang được thực thi và được hệ điều hành quản lý thông qua Process ID (PID).

Các lệnh thường dùng:

### ps

Hiển thị danh sách process.

```bash
ps aux
```

### htop

Theo dõi process theo thời gian thực với giao diện trực quan.

### kill

Dừng một process theo PID.

```bash
kill 1234
```

### jobs

Hiển thị các tiến trình đang chạy trong shell hiện tại.

### nohup

Chạy chương trình ngay cả khi đóng Terminal.

```bash
nohup java -jar app.jar &
```

---

## 5. Text Processing

Linux cung cấp nhiều công cụ xử lý văn bản mạnh mẽ.

### grep

Tìm kiếm dòng chứa chuỗi ký tự.

```bash
grep "ERROR" app.log
```

### sed

Chỉnh sửa văn bản theo dòng.

```bash
sed 's/java/spring/g' file.txt
```

### awk

Xử lý dữ liệu theo từng cột.

```bash
awk '{print $1}'
```

### cut

Cắt dữ liệu theo cột.

```bash
cut -d',' -f2 data.csv
```

### sort

Sắp xếp dữ liệu.

```bash
sort file.txt
```

### uniq

Loại bỏ các dòng trùng lặp liên tiếp.

```bash
sort file.txt | uniq
```

Các công cụ này thường được sử dụng để phân tích log, xử lý dữ liệu và hỗ trợ tự động hóa.

---

## 6. Network Utilities

Các công cụ mạng giúp kiểm tra kết nối và giao tiếp giữa các dịch vụ.

### netstat

Hiển thị các kết nối mạng và cổng đang mở.

### ss

Phiên bản hiện đại và nhanh hơn của netstat.

### curl

Gửi HTTP Request để kiểm tra API.

```bash
curl http://localhost:8080/api/users
```

### wget

Tải file từ Internet.

```bash
wget https://example.com/file.zip
```

---

## 7. System Monitoring

Giám sát tài nguyên hệ thống giúp theo dõi hiệu năng của máy chủ.

### df

Hiển thị dung lượng ổ đĩa.

### du

Hiển thị dung lượng của thư mục hoặc file.

### free

Kiểm tra bộ nhớ RAM.

### top

Theo dõi CPU, RAM và process theo thời gian thực.

### iostat

Theo dõi hoạt động của CPU và thiết bị lưu trữ.

---

## 8. Shell Scripting và Environment Variables

Shell Script là tập hợp các lệnh Linux được lưu trong một tệp `.sh` để thực hiện tự động nhiều thao tác.

Ví dụ:

```bash
#!/bin/bash

echo "Hello Linux"
```

Environment Variable là các biến được hệ điều hành sử dụng để lưu thông tin cấu hình.

Một số biến phổ biến:

- `PATH`
- `HOME`
- `USER`
- `JAVA_HOME`

Các lệnh thường dùng:

```bash
echo $PATH
```

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
```

Shell Script thường được sử dụng để tự động hóa quá trình build, deploy, backup và quản lý hệ thống.

---

# III. Linux Theory

## 1. Process Lifecycle

Vòng đời của một Process trên Linux thường gồm các bước:

1. **fork()**

Process cha tạo ra Process con bằng lời gọi hệ thống `fork()`.

2. **exec()**

Process con nạp chương trình mới vào bộ nhớ và bắt đầu thực thi.

3. **Running**

Process được CPU cấp phát tài nguyên để thực hiện công việc.

4. **wait()**

Process cha chờ Process con hoàn thành và thu hồi tài nguyên.

5. **Terminate**

Process kết thúc sau khi hoàn thành hoặc bị dừng.

6. **Zombie Process**

Là Process đã kết thúc nhưng Process cha chưa thu hồi trạng thái của nó. Zombie không sử dụng CPU nhưng vẫn chiếm một mục trong bảng Process.

---

## 2. File Permissions

Quyền truy cập của Linux được biểu diễn bằng ba nhóm:

- Owner
- Group
- Other

Mỗi nhóm có ba quyền:

| Quyền | Ý nghĩa |
|--------|----------|
| r | Read |
| w | Write |
| x | Execute |

Ví dụ:

```
-rwxr-xr--
```

Trong đó:

- Owner có quyền đọc, ghi và thực thi.
- Group có quyền đọc và thực thi.
- Other chỉ có quyền đọc.

Hệ thống phân quyền giúp bảo vệ dữ liệu và hạn chế truy cập trái phép.

---

## 3. I/O Redirection

Linux quản lý dữ liệu vào và ra thông qua ba luồng chuẩn:

| Luồng | Mô tả |
|-------|-------|
| stdin | Dữ liệu đầu vào |
| stdout | Dữ liệu đầu ra |
| stderr | Thông báo lỗi |

Các toán tử chuyển hướng:

- `>` ghi đè đầu ra vào file.
- `>>` ghi nối vào file.
- `<` đọc dữ liệu từ file.
- `|` truyền đầu ra của lệnh trước làm đầu vào cho lệnh sau.

Ví dụ:

```bash
grep ERROR app.log | sort
```

I/O Redirection giúp kết hợp nhiều lệnh để xử lý dữ liệu một cách hiệu quả.

---

## 4. System Logs

System Log là nơi lưu lại các sự kiện xảy ra trong hệ điều hành và ứng dụng.

Một số vị trí quan trọng:

| Đường dẫn | Chức năng |
|-----------|-----------|
| `/var/log` | Thư mục chứa log hệ thống |
| `/var/log/syslog` | Log hệ thống |
| `/var/log/auth.log` | Log xác thực người dùng |

### journalctl

`journalctl` là công cụ xem log của systemd.

Ví dụ:

```bash
journalctl
```

```bash
journalctl -f
```

Log hệ thống giúp theo dõi lỗi, kiểm tra hoạt động của dịch vụ và hỗ trợ quá trình phân tích, xử lý sự cố.

---
