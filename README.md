# Java

## Java Basics

### I. [ JDK [ JRE [ JVM ] ] ]

### II. String pool

1. `String s1 = "abc";` : Tạo chuỗi trong string pool
2. `String s2 = new String("abc");` : Tạo chuỗi trong heap

=> `s1 == s2` là `false` (khác địa chỉ vùng nhớ), `s1.equals(s2)` là `true` (cùng nội dung)
=> `String.intern()`: đưa chuỗi vào string pool để tối ưu

### III. Number

1. `int a = 1_000_000;` : Tạo số nguyên với dấu gạch dưới để dễ đọc

### IV. switch (arrow, yield)

```java
        var result = switch (month) {
            case 1, 3, 5, 7, 8, 10, 12 -> "31 days";
            case 4, 6, 9, 11 -> "30 days";
            case 2 -> "28 or 29 days";
            default -> "Invalid month";
        };
```

Hoặc với yield

```java
        var result = switch (month) {
            case 1, 3, 5, 7, 8, 10, 12 -> { yield "31 days" };
            case 4, 6, 9, 11 -> { yield "30 days" };
            case 2 -> { yield "28 or 29 days" };
            default -> { yield "Invalid month" };
        };
```

### V. transient

- Bỏ qua biến trong quá trình Serialization để bảo mật/tối ưu.

```java
public class Student implements Serializable {
    transient String name;    // không được serialize
    int age;                  // được serialize

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

### VI. Multi-threading

1. `volatile`
   - Là một Modifier áp dụng cho biến. Đảm bảo tính nhất quán dữ liệu của biến giữa các Thread khác nhau.
2. `synchronized`
   - Là một Locking mechanism áp dụng cho Hàm/Khối lệnh. Đảm bảo chỉ có một luồng truy cập được vào vùng code được bảo vệ tại một thời điểm.
3. `Atomic Variables`
   - Là một Class trong Java hỗ trợ thực hiện các thao tác nguyên tử (Atomicity) trên các biến thông thường mà không cần sử dụng `synchronized`.

---

## Java OOP

### I. Functional Interface

- Interface chỉ có 1 abstract method
- Có thể sử dụng @FunctionalInterface
- Có thể sử dụng Lambda Expression

```java
@FunctionalInterface
interface MyInterface {
    void myMethod();
}

MyInterface myInterface = () -> System.out.println("Hello World");
myInterface.myMethod();
```

- Các nhóm Functional Interface cốt lõi trong gói java.util.function:
  - **Nhóm Function (Ánh xạ / Chuyển đổi dữ liệu)**: `Function<T, R>`, `BiFunction<T, U, R>`, `BinaryOperator<T>`, `UnaryOperator<T>`.
  - **Nhóm Consumers (Tiêu thụ dữ liệu)**: `Consumer<T>`, `BiConsumer<T, U>`, `IntConsumer`, `LongConsumer`, `DoubleConsumer`, `Stream.forEach()`
  - **Nhóm Suppliers (Cung cấp dữ liệu)**: `Supplier<T>`, `BooleanSupplier`, `IntSupplier`, `LongSupplier`, `DoubleSupplier`.
  - **Nhóm Predicates (Kiểm tra điều kiện)**: `Predicate<T>`, `BiPredicate<T, U>`, `IntPredicate`, `LongPredicate`, `DoublePredicate`.
  - **Nhóm Comparator (So sánh đối tượng)**: `Comparator<T>`.

### II. Stream API

1. `filter()`
2. `map()`
3. `reduce()`

### III. default method

- Mở rộng tính năng cho một Interface đang có sẵn trong dự án lớn mà không muốn làm ảnh hưởng (gây lỗi compile) đến các lớp con đã viết từ trước

### IV. Double Colon Operator in Java (::)

- Là cú pháp viết ngắn gọn (syntactic sugar) trong Java để biểu diễn một Method Reference.
- Có thể sử dụng để thay thế cho Lambda Expression khi cần truyền một method có sẵn vào một Functional Interface.

### V. Các loại Double Colon Operator

1. **Tham chiếu tới một static method:**

   ```java
   // Lambda
   list.forEach(e -> System.out.println(e));
   // Double Colon
   list.forEach(System.out::println);
   ```

2. **Tham chiếu tới một instance method:**

   ```java
   // Lambda
   Comparator<String> c = (s1, s2) -> s1.compareTo(s2);
   // Double Colon
   Comparator<String> c = String::compareTo;
   ```

3. **Tham chiếu tới constructor:**

   ```java
   // Lambda
   Supplier<MyClass> s = () -> new MyClass();
   // Double Colon
   Supplier<MyClass> s = MyClass::new;
   ```

4. **Tham chiếu tới instance method với tham số đặc biệt (this, super):**

   ```java
   // Tham chiếu tới method của đối tượng hiện tại
   list.forEach(this::myMethod);
   // Tham chiếu tới method của đối tượng cha
   super::myMethod;
   ```

### VI. Optional

### VII. Text Blocks

```java
   String html = """
                  <html>
                     <body>
                        <h1>Hello, World!</h1>
                     </body>
                  </html>
                  """;
   System.out.println(html);
```

### VIII. isBlank()
