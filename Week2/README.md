# Week 2 - Collections, Design Patterns & Testing

## Giới thiệu

Trong tuần thứ hai của chương trình thực tập, mục tiêu là tìm hiểu sâu hơn về cơ chế hoạt động của Java Collection Framework, các Design Pattern phổ biến và các kiến thức nền tảng về kiểm thử phần mềm (Testing). Đây là những nội dung quan trọng giúp xây dựng ứng dụng có hiệu năng tốt, dễ bảo trì và đảm bảo chất lượng trước khi triển khai.

---

# I. Java Collections

## 1. Collection Framework Internals

Collection Framework là tập hợp các Interface và Class hỗ trợ lưu trữ, quản lý và xử lý dữ liệu. Việc hiểu cơ chế hoạt động bên trong (Internals) giúp lựa chọn cấu trúc dữ liệu phù hợp nhằm tối ưu hiệu năng và bộ nhớ.

---

## 2. ArrayList Internals

ArrayList được cài đặt dựa trên mảng động (Dynamic Array). Khi số lượng phần tử vượt quá dung lượng hiện tại, ArrayList sẽ tạo một mảng mới có kích thước lớn hơn và sao chép toàn bộ dữ liệu sang mảng mới.

### Đặc điểm

- Truy cập phần tử theo chỉ số rất nhanh (O(1)).
- Thêm phần tử cuối danh sách có hiệu năng tốt.
- Chèn hoặc xóa ở giữa danh sách cần dịch chuyển dữ liệu nên chậm hơn.

### Khi sử dụng

- Danh sách thường xuyên đọc dữ liệu.
- Ít thao tác thêm hoặc xóa ở giữa.

---

## 3. HashMap Internals

HashMap lưu dữ liệu theo cặp **Key - Value** và sử dụng bảng băm (Hash Table) để tăng tốc độ tìm kiếm.

Quá trình lưu trữ gồm các bước:

1. Tính `hashCode()` của Key.
2. Chuyển đổi thành chỉ số (Bucket Index).
3. Lưu Entry vào Bucket tương ứng.
4. Nếu xảy ra Collision sẽ xử lý bằng Linked List hoặc Red-Black Tree (Java 8 trở lên).

### Đặc điểm

- Tra cứu rất nhanh trong điều kiện bình thường.
- Không đảm bảo thứ tự dữ liệu.
- Không thread-safe.

### Khi sử dụng

- Tra cứu dữ liệu theo khóa.
- Cache dữ liệu.
- Lưu cấu hình hoặc ánh xạ thông tin.

---

## 4. HashSet Internals

HashSet được xây dựng dựa trên HashMap. Mỗi phần tử trong HashSet được lưu dưới dạng Key của HashMap, còn Value là một đối tượng giả (Dummy Object).

### Đặc điểm

- Không cho phép phần tử trùng lặp.
- Không đảm bảo thứ tự.
- Tìm kiếm nhanh.

### Khi sử dụng

- Loại bỏ dữ liệu trùng lặp.
- Kiểm tra sự tồn tại của phần tử.

---

## 5. HashCode và Equals Contract

### hashCode()

Là phương thức tạo ra giá trị băm (Hash Value) của đối tượng nhằm xác định Bucket trong HashMap hoặc HashSet.

### equals()

Được sử dụng để xác định hai đối tượng có bằng nhau hay không.

### Contract giữa hashCode() và equals()

- Nếu hai đối tượng bằng nhau theo `equals()` thì phải có cùng `hashCode()`.
- Hai đối tượng có cùng `hashCode()` chưa chắc bằng nhau.
- Khi ghi đè `equals()` nên ghi đè cả `hashCode()`.

Việc tuân thủ contract giúp HashMap và HashSet hoạt động chính xác.

---

## 6. Concurrent Collections

Concurrent Collections là các Collection được thiết kế dành cho môi trường đa luồng, giúp nhiều Thread có thể truy cập dữ liệu an toàn mà vẫn đảm bảo hiệu năng.

### ConcurrentHashMap

ConcurrentHashMap là phiên bản thread-safe của HashMap.

Đặc điểm:

- Cho phép nhiều Thread đọc đồng thời.
- Giảm xung đột so với Hashtable.
- Hiệu năng cao trong môi trường đa luồng.

### BlockingQueue

BlockingQueue là hàng đợi hỗ trợ đồng bộ giữa Producer và Consumer.

Đặc điểm:

- Thread sẽ chờ nếu Queue đầy hoặc rỗng.
- Hỗ trợ giao tiếp giữa nhiều Thread.
- Được sử dụng nhiều trong Thread Pool và Message Queue.

---

# II. Design Patterns

## 1. Design Pattern là gì?

Design Pattern là các giải pháp thiết kế đã được kiểm chứng nhằm giải quyết những vấn đề thường gặp trong phát triển phần mềm. Việc áp dụng Design Pattern giúp mã nguồn dễ mở rộng, dễ bảo trì và giảm sự phụ thuộc giữa các thành phần.

---

## 2. Singleton Pattern

Singleton đảm bảo chỉ tồn tại một đối tượng duy nhất của một lớp trong suốt thời gian chạy chương trình.

### Khi sử dụng

- Configuration.
- Logger.
- Cache.
- Connection Manager.

### Ưu điểm

- Tiết kiệm tài nguyên.
- Quản lý trạng thái tập trung.

---

## 3. Factory Pattern

Factory Pattern tạo đối tượng thông qua một lớp Factory thay vì khởi tạo trực tiếp bằng từ khóa `new`.

### Ưu điểm

- Giảm phụ thuộc vào lớp cụ thể.
- Dễ mở rộng khi thêm loại đối tượng mới.

### Ứng dụng

- Spring Bean Factory.
- Object Creation.
- Parser.
- Database Driver.

---

## 4. Observer Pattern

Observer Pattern xây dựng mối quan hệ một-nhiều giữa các đối tượng. Khi trạng thái của Subject thay đổi, các Observer sẽ được thông báo tự động.

### Ứng dụng

- Event Listener.
- Notification System.
- GUI Event.
- Message Event.

---

## 5. Strategy Pattern

Strategy Pattern đóng gói nhiều thuật toán khác nhau thành các Strategy riêng biệt và có thể thay đổi trong quá trình chạy.

### Ưu điểm

- Loại bỏ nhiều câu lệnh if-else.
- Dễ mở rộng thuật toán.
- Tuân thủ Open/Closed Principle.

### Ứng dụng

- Thanh toán.
- Sắp xếp dữ liệu.
- Tính phí vận chuyển.
- Xác thực người dùng.

---

# III. Testing

## 1. Testing là gì?

Testing là quá trình kiểm tra phần mềm nhằm phát hiện lỗi và đảm bảo chương trình hoạt động đúng với yêu cầu.

Mục tiêu của Testing:

- Phát hiện lỗi sớm.
- Đảm bảo chất lượng phần mềm.
- Hạn chế lỗi khi triển khai.

---

## 2. Unit Testing

Unit Testing là quá trình kiểm thử một thành phần nhỏ nhất của chương trình (thường là một Method hoặc Class) một cách độc lập.

### Đặc điểm

- Thực thi nhanh.
- Không phụ thuộc Database hoặc API.
- Dễ xác định vị trí lỗi.

### Nguyên tắc

- Mỗi Test chỉ kiểm tra một chức năng.
- Độc lập với các Test khác.
- Có thể chạy nhiều lần với cùng kết quả.

---

## 3. JUnit 5

JUnit 5 là framework phổ biến dùng để viết Unit Test trong Java.

Một số Annotation thường dùng:

| Annotation | Ý nghĩa |
|------------|----------|
| @Test | Đánh dấu phương thức kiểm thử |
| @BeforeEach | Chạy trước mỗi Test |
| @AfterEach | Chạy sau mỗi Test |
| @BeforeAll | Chạy một lần trước toàn bộ Test |
| @AfterAll | Chạy một lần sau toàn bộ Test |

JUnit 5 hỗ trợ Assertions để so sánh kết quả mong đợi với kết quả thực tế.

---

## 4. Mocking

Mocking là kỹ thuật tạo các đối tượng giả lập để thay thế các thành phần phụ thuộc trong quá trình Unit Test.

Ví dụ:

- Database.
- REST API.
- File System.
- Email Service.

Mục đích:

- Giảm phụ thuộc.
- Kiểm thử nhanh hơn.
- Kiểm tra từng thành phần độc lập.

Mockito là thư viện Mocking phổ biến trong Java.

---

## 5. Integration Testing

Integration Testing kiểm tra sự phối hợp giữa nhiều thành phần của hệ thống.

Ví dụ:

- Controller và Service.
- Service và Repository.
- Repository và Database.

Mục tiêu:

- Kiểm tra luồng xử lý hoàn chỉnh.
- Phát hiện lỗi tích hợp.
- Đảm bảo các module hoạt động chính xác khi kết hợp.

---

## 6. Test Coverage

Test Coverage là tỷ lệ mã nguồn được thực thi trong quá trình chạy Test.

Một số loại Coverage:

- Line Coverage.
- Branch Coverage.
- Method Coverage.
- Class Coverage.

Coverage cao giúp tăng mức độ tin cậy nhưng không đảm bảo chương trình hoàn toàn không có lỗi.

---

## 7. Quality Metrics

Quality Metrics là các chỉ số đánh giá chất lượng của mã nguồn và hệ thống kiểm thử.

Một số chỉ số phổ biến:

- Test Coverage.
- Defect Density.
- Pass Rate.
- Code Complexity.
- Code Duplication.
- Maintainability.

Các chỉ số này giúp đánh giá mức độ ổn định và khả năng bảo trì của phần mềm.

---

# Tổng kết

Trong tuần thứ hai, tôi đã tìm hiểu cơ chế hoạt động của các Collection phổ biến trong Java, nguyên lý của HashMap và HashSet, mối quan hệ giữa `hashCode()` và `equals()`, cùng với các Collection hỗ trợ đa luồng. Bên cạnh đó, tôi nghiên cứu bốn Design Pattern cơ bản gồm Singleton, Factory, Observer và Strategy để hiểu cách tổ chức và mở rộng mã nguồn hiệu quả.

Về Testing, tôi tìm hiểu các nguyên tắc của Unit Testing, cách sử dụng JUnit 5, kỹ thuật Mocking, chiến lược Integration Testing và các chỉ số đánh giá chất lượng như Test Coverage và Quality Metrics. Những kiến thức này là nền tảng quan trọng để phát triển các ứng dụng Java có chất lượng, dễ kiểm thử và dễ bảo trì.
