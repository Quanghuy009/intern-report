# Week 3 - Concurrency

## Mục tiêu

- Hiểu khái niệm lập trình đồng thời (Concurrency).
- Nắm được vòng đời và cách quản lý Thread trong Java.
- Hiểu cách sử dụng Thread Pool và `ExecutorService`.
- Biết cách đồng bộ dữ liệu bằng `synchronized`, `Lock` và `Atomic`.
- Làm quen với lập trình bất đồng bộ bằng `CompletableFuture`.
- Tìm hiểu các khái niệm cơ bản của Reactive Programming.

---

# 1. Tổng quan về Concurrency

## 1.1 Concurrency là gì?

Concurrency (Lập trình đồng thời) là khả năng cho phép nhiều tác vụ được thực hiện trong cùng một khoảng thời gian. Thay vì thực hiện lần lượt từng công việc, chương trình có thể xử lý nhiều công việc đồng thời nhằm tận dụng tài nguyên hệ thống và cải thiện hiệu suất.

Ví dụ:

- Tải dữ liệu từ Database.
- Gửi Email.
- Ghi Log.

Ba tác vụ này có thể được thực hiện đồng thời thay vì tuần tự.

### Lợi ích

- Tăng hiệu năng chương trình.
- Tận dụng CPU đa nhân.
- Giảm thời gian chờ của người dùng.
- Xử lý được nhiều yêu cầu cùng lúc.

---

## 1.2 Concurrency và Parallelism

### Concurrency

- Nhiều tác vụ cùng được xử lý trong một khoảng thời gian.
- CPU có thể luân phiên thực thi các tác vụ.
- Không bắt buộc phải có nhiều CPU Core.

### Parallelism

- Nhiều tác vụ thực sự chạy cùng lúc.
- Thường yêu cầu CPU nhiều nhân (Multi-core).

| Concurrency | Parallelism |
|-------------|-------------|
| Nhiều tác vụ cùng tiến triển | Nhiều tác vụ chạy thực sự cùng lúc |
| Có thể dùng một CPU | Cần nhiều CPU/Core |
| CPU luân phiên xử lý | Các Core xử lý song song |

---

## 1.3 Đồng bộ và Bất đồng bộ

### Đồng bộ (Synchronous)

Một tác vụ phải hoàn thành trước khi tác vụ tiếp theo được thực hiện.

Ví dụ:

```text
Đọc File
    ↓
Xử lý File
    ↓
Gửi Email
```

### Bất đồng bộ (Asynchronous)

Một tác vụ được giao cho luồng khác thực hiện, trong khi luồng hiện tại vẫn tiếp tục công việc của mình.

Ví dụ:

```text
Đọc File  ──────────────

Main Thread
        ↓
Tiếp tục xử lý dữ liệu
```

---

# 2. Thread Lifecycle và Thread Management

## 2.1 Thread là gì?

Thread là đơn vị thực thi nhỏ nhất trong một Process.

Một chương trình Java luôn có ít nhất một Thread là Main Thread.

Ngoài ra còn có thể tạo thêm nhiều Thread để xử lý đồng thời nhiều công việc.

Ví dụ:

- Thread xử lý Request.
- Thread gửi Email.
- Thread ghi Log.
- Thread xử lý File.

---

## 2.2 Vòng đời của Thread

Một Thread trong Java trải qua các trạng thái sau:

```text
NEW
 │
 │ start()
 ▼
RUNNABLE
 │
 ▼
RUNNING
 │
 ├──────────────┐
 │              │
 ▼              │
WAITING         │
BLOCKED         │
TIMED_WAITING   │
 │              │
 └──────────────┘
 │
 ▼
TERMINATED
```

### NEW

Thread vừa được tạo.

```java
Thread t = new Thread();
```

---

### RUNNABLE

Thread đã được gọi `start()` và sẵn sàng được CPU thực thi.

```java
t.start();
```

---

### BLOCKED

Thread đang chờ lấy Lock của một đối tượng.

---

### WAITING

Thread chờ vô thời hạn.

Ví dụ:

```java
thread.join();

object.wait();
```

---

### TIMED_WAITING

Thread chờ trong khoảng thời gian xác định.

Ví dụ:

```java
Thread.sleep(3000);
```

---

### TERMINATED

Thread đã thực hiện xong và kết thúc.

---

## 2.3 Quản lý Thread

Một số phương thức quan trọng:

| Phương thức | Ý nghĩa |
|-------------|----------|
| start() | Khởi động Thread |
| run() | Nội dung công việc |
| sleep() | Tạm dừng Thread |
| join() | Chờ Thread khác hoàn thành |
| interrupt() | Yêu cầu dừng Thread |

---

# 3. Thread Pool và ExecutorService

## 3.1 Vì sao cần Thread Pool?

Nếu mỗi Request đều tạo một Thread mới sẽ gây:

- Tốn bộ nhớ.
- Tạo Thread chậm.
- Giảm hiệu năng.
- Có thể gây OutOfMemoryError.

Thread Pool giúp tái sử dụng các Thread có sẵn.

---

## 3.2 ExecutorService

`ExecutorService` là API quản lý Thread Pool trong Java.

Ví dụ:

```java
ExecutorService executor =
        Executors.newFixedThreadPool(4);

executor.submit(() -> {
    System.out.println("Execute Task");
});

executor.shutdown();
```

Thay vì tự tạo và quản lý Thread, `ExecutorService` sẽ thực hiện việc đó.

---

## 3.3 Các loại Thread Pool

### FixedThreadPool

Số lượng Thread cố định.

```java
Executors.newFixedThreadPool(4);
```

---

### CachedThreadPool

Tự động tạo hoặc tái sử dụng Thread khi cần.

```java
Executors.newCachedThreadPool();
```

---

### SingleThreadExecutor

Chỉ có một Thread thực thi.

```java
Executors.newSingleThreadExecutor();
```

---

### ScheduledThreadPool

Thực hiện các công việc theo lịch.

```java
Executors.newScheduledThreadPool(2);
```

Ví dụ:

- Backup Database.
- Gửi Email định kỳ.

---

# 4. Synchronization

## 4.1 Race Condition

Race Condition xảy ra khi nhiều Thread cùng truy cập và thay đổi một vùng dữ liệu.

Ví dụ:

```java
balance = balance - 100;
```

Nếu hai Thread cùng thực hiện đồng thời, kết quả có thể sai.

---

## 4.2 synchronized

Từ khóa `synchronized` giúp đảm bảo chỉ một Thread được phép truy cập vùng dữ liệu tại một thời điểm.

Ví dụ:

```java
public synchronized void withdraw() {

}
```

Hoặc:

```java
synchronized(lock){

}
```

Ưu điểm:

- Dễ sử dụng.
- Đảm bảo Thread Safety.

Nhược điểm:

- Có thể làm giảm hiệu năng khi nhiều Thread phải chờ Lock.

---

## 4.3 Lock

Lớp `ReentrantLock` cung cấp cơ chế khóa linh hoạt hơn.

Ví dụ:

```java
Lock lock = new ReentrantLock();

lock.lock();

try {

} finally {
    lock.unlock();
}
```

Ưu điểm:

- Có thể thử lấy Lock (`tryLock()`).
- Có thể đặt thời gian chờ.
- Có thể ngắt khi đang chờ Lock.

---

## 4.4 Atomic Classes

Các lớp Atomic sử dụng cơ chế CAS (Compare-And-Set) để thực hiện các phép toán nguyên tử mà không cần khóa.

Ví dụ:

```java
AtomicInteger counter = new AtomicInteger();

counter.incrementAndGet();
```

Một số lớp thường dùng:

- AtomicInteger
- AtomicLong
- AtomicBoolean
- AtomicReference

Ưu điểm:

- Nhanh hơn synchronized trong các phép toán đơn giản.
- Không cần Lock.

---

# 5. CompletableFuture

## 5.1 CompletableFuture là gì?

`CompletableFuture` là API hỗ trợ lập trình bất đồng bộ trong Java.

Cho phép thực hiện nhiều tác vụ song song và xử lý kết quả sau khi hoàn thành.

---

## 5.2 Tạo CompletableFuture

```java
CompletableFuture<Void> future =
        CompletableFuture.runAsync(() -> {
            System.out.println("Running...");
        });
```

---

## 5.3 Trả về kết quả

```java
CompletableFuture<String> future =
        CompletableFuture.supplyAsync(() -> {
            return "Hello";
        });
```

Lấy kết quả:

```java
future.get();

future.join();
```

---

## 5.4 Kết hợp nhiều Future

```java
CompletableFuture.allOf(f1, f2, f3);
```

Hoặc:

```java
CompletableFuture.anyOf(f1, f2);
```

---

## 5.5 Chuỗi xử lý

```java
future
    .thenApply(...)
    .thenAccept(...)
    .exceptionally(...);
```

Cho phép xây dựng pipeline xử lý dữ liệu bất đồng bộ.

---

# 6. Reactive Programming Basics

## 6.1 Reactive Programming là gì?

Reactive Programming là mô hình lập trình xử lý dữ liệu dưới dạng luồng (Data Stream), hướng đến các ứng dụng:

- Non-blocking
- Event-driven
- Responsive
- Scalable

Reactive giúp tận dụng tài nguyên hiệu quả khi hệ thống phải xử lý nhiều tác vụ I/O.

---

## 6.2 Các thành phần cơ bản

### Publisher

Nguồn phát dữ liệu.

### Subscriber

Đối tượng nhận dữ liệu.

### Subscription

Quản lý việc đăng ký và hủy đăng ký.

### Backpressure

Điều khiển tốc độ truyền dữ liệu giữa Publisher và Subscriber để tránh quá tải.

---

## 6.3 Mono và Flux

Trong Project Reactor:

### Mono

Trả về tối đa một giá trị.

```java
Mono<String> mono = Mono.just("Hello");
```

---

### Flux

Trả về nhiều giá trị.

```java
Flux<Integer> flux = Flux.just(1,2,3,4);
```

---

## 6.4 Khi nào sử dụng Reactive?

Reactive phù hợp với:

- Chat Application.
- Notification Service.
- API Gateway.
- Streaming Data.
- Hệ thống có nhiều thao tác I/O.

