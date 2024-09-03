# 8 DESIGN PATTERNS

## Creational Patterns: 
    liên quan đến việc tạo ra các đối tượng. Chúng cung cấp các cơ chế để khởi tạo các đối tượng một cách linh hoạt và hiệu quả.

### Singleton: 
    Đảm bảo rằng chỉ có một thể hiện duy nhất của lớp và cung cấp điểm truy cập toàn cục cho đối tượng đó.

### Factory Method: 
    Cung cấp một giao diện để tạo ra các đối tượng trong một lớp cơ sở, nhưng cho phép các lớp con quyết định lớp nào sẽ được khởi tạo.

### Abstract Factory: 
    Cung cấp một giao diện để tạo ra các họ đối tượng liên quan hoặc phụ thuộc mà không cần chỉ rõ lớp cụ thể.

### Builder: 
    Tách việc tạo đối tượng phức tạp thành các bước đơn giản, cho phép tái sử dụng quy trình tạo ra đối tượng mà không phụ thuộc vào lớp cụ thể.

### Prototype: 
    Tạo các đối tượng mới bằng cách sao chép đối tượng hiện có (prototype) thay vì tạo mới từ đầu.

## Structural Patterns: liên quan đến cách các lớp và đối tượng được tổ chức và kết hợp với nhau.

### Adapter: 
    Chuyển đổi giao diện của một lớp thành giao diện mà client mong đợi, cho phép các lớp không tương thích làm việc cùng nhau.

### Bridge: 
    Tách sự trừu tượng khỏi việc thực hiện, cho phép chúng phát triển độc lập.

### Composite:
    Hợp nhất các đối tượng thành một cấu trúc cây để xử lý các đối tượng đơn lẻ và các nhóm đối tượng theo cách giống nhau.

### Decorator: 
    Thêm chức năng cho các đối tượng một cách linh hoạt mà không cần thay đổi lớp của đối tượng đó.

### Facade: 
    Cung cấp một giao diện đơn giản cho một tập hợp các giao diện phức tạp trong một hệ thống, giúp giảm độ phức tạp của mã nguồn.

### Flyweight: 
    Giảm số lượng đối tượng cần tạo ra bằng cách chia sẻ các đối tượng tương tự nhau, giảm chi phí bộ nhớ.

### Proxy: 
    Cung cấp một đại diện hoặc trình điều khiển cho một đối tượng khác để kiểm soát việc truy cập vào đối tượng đó.

## Behavioral Patterns: liên quan đến cách các đối tượng tương tác và giao tiếp với nhau.

### Chain of Responsibility: 
    Cho phép một yêu cầu được chuyển qua một chuỗi các đối tượng để xử lý, mỗi đối tượng có thể xử lý yêu cầu hoặc chuyển nó cho đối tượng kế tiếp.

### Command: 
    Đóng gói một yêu cầu dưới dạng đối tượng, bao gồm tất cả thông tin cần thiết để thực hiện yêu cầu, giúp hỗ trợ việc thực hiện các hành động, huỷ bỏ hoặc ghi lại các hành động.

### Interpreter: 
    Cung cấp một cách để đánh giá ngữ nghĩa của một ngôn ngữ hoặc biểu thức.

### Iterator: 
    Cung cấp một cách để tuần tự truy cập các phần tử của một tập hợp mà không cần lộ cấu trúc bên trong của nó.

### Mediator: 
    Định nghĩa một đối tượng để giao tiếp giữa các đối tượng khác mà không cần các đối tượng giao tiếp trực tiếp với nhau.

### Memento: 
    Cho phép khôi phục trạng thái của một đối tượng mà không cần vi phạm tính đóng gói của nó.

### Observer: 
    Cho phép một đối tượng (subject) thông báo cho các đối tượng khác (observers) khi có sự thay đổi trong trạng thái của nó.

### State: 
    Cho phép một đối tượng thay đổi hành vi của mình khi trạng thái của nó thay đổi, đối tượng sẽ có vẻ như đã thay đổi lớp.

### Strategy: 
    Định nghĩa một tập hợp các thuật toán, đóng gói từng thuật toán, và làm cho chúng có thể thay thế lẫn nhau.

### Template Method: 
    Xác định cấu trúc của một thuật toán trong một phương thức, để các lớp con có thể định nghĩa các bước cụ thể của thuật toán mà không thay đổi cấu trúc chung.

### Visitor: 
    Cho phép thêm các hành vi mới vào các đối tượng mà không thay đổi các lớp của đối tượng đó.