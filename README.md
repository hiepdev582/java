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
