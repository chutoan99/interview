# DESIGN PATTERNS

## Creational Patterns: 
là một nhóm các mẫu thiết kế tập trung vào việc khởi tạo object. Giúp object linh hoạt hơn và ít tight-coupling (liên kết ràng buộc) hơn với client code. 

Các Creational design patterns thúc đẩy việc tái sử dụng code, khả năng bảo trì và khả năng mở rộng, tạo điều kiện thuận lợi cho việc tạo các object theo cách hiệu quả và có khả năng kiểm soát nhằm đáp ứng các yêu cầu đa dạng của ứng dụng.

### `1. Singleton` 
Singleton là một mẫu thiết kế sáng tạo cho phép bạn đảm bảo rằng một class chỉ có một instance, đồng thời cung cấp một điểm truy cập toàn cầu cho phiên bản này.
```typescript
class Singleton {
    private static instance: Singleton;
    public data: string;
    private constructor() {
        this.data = "Singleton Data";
    }
    // lấy instance duy nhất của Singleton
    public static getInstance(): Singleton {
        if (!Singleton.instance) {
            Singleton.instance = new Singleton();
        }
        return Singleton.instance;
    }
}

const singleton1 = Singleton.getInstance();
const singleton2 = Singleton.getInstance();
console.log(singleton1 === singleton2); // true: cả hai đều là cùng một instance
```
Lợi ích:
- Kiểm soát việc tạo đối tượng: Chỉ một instance duy nhất của Singleton được tạo ra, giúp kiểm soát việc truy cập tài nguyên chung hoặc cài đặt toàn cục trong ứng dụng.
- Dễ bảo trì: Dễ dàng quản lý các thành phần toàn cục mà không cần phải khởi tạo lại nhiều lần.


### `2. Factory Method` 
Đây là một mẫu thiết kế rất hữu ích và được xem là một mẫu giúp tạo instance của các object trong Java. Nó cung cấp khả năng kiểm soát tốt hơn đối với quá trình tạo object sau đó là constructor. 
```typescript
interface Shape { draw(): void}
class Circle implements Shape {
    public draw(): void { console.log("Drawing a Circle");}
}
class Square implements Shape {
    public draw(): void { console.log("Drawing a Square");}
}
class Rectangle implements Shape {
    public draw(): void { console.log("Drawing a Rectangle");}
}
class ShapeFactory {
    public static createShape(type: string): Shape | null {
        switch (type) {
            case "circle": return new Circle();
            case "square": return new Square();
            case "rectangle": return new Rectangle();
            default: return null;
        }
    }
}

// Sử dụng ShapeFactory để tạo các đối tượng Shape
const shape1 = ShapeFactory.createShape("circle");
shape1?.draw(); // Output: Drawing a Circle

const shape2 = ShapeFactory.createShape("square");
shape2?.draw(); // Output: Drawing a Square

const shape3 = ShapeFactory.createShape("rectangle");
shape3?.draw(); // Output: Drawing a Rectangle

```
Lợi ích
- Tách biệt mã khởi tạo: Việc tạo đối tượng được tách biệt khỏi phần mã sử dụng đối tượng, giúp mã dễ bảo trì và mở rộng.
- Dễ dàng mở rộng: Khi có một hình dạng mới, bạn chỉ cần thêm lớp mới và cập nhật ShapeFactory mà không cần thay đổi các phần mã khác.
- Đảm bảo tuân theo nguyên tắc Open/Closed: Bạn có thể mở rộng hệ thống (bằng cách thêm hình dạng mới) mà không cần sửa đổi mã hiện có.

### `3. Abstract Factory` 
Đây là phần mở rộng của mẫu thiết kế trước đó. Nó bổ sung thêm một lớp abstract (trừu tượng) khác trên mẫu thiết kế Factory. Trong trường hợp này, bản thân Factory là abtract (trừu tượng), cho phép các chương trình chọn cách triển khai Factory khác nhau, tạo ra đặc tính khác nhau của cùng một sản phẩm tùy thuộc vào localization và các yêu cầu khác. 

### `4. Builder` 
Builder là một mẫu thiết kế sáng tạo cho phép bạn xây dựng các object phức tạp theo từng bước. Mẫu này cho phép bạn tạo ra các kiểu và cách biểu diễn khác nhau của một object bằng cách sử dụng cùng một construction code.

```typescript
class House {
    public floors: number;
    public hasGarden: boolean;
    public hasSwimmingPool: boolean;
    constructor(builder: HouseBuilder) {
        this.floors = builder.floors;
        this.hasGarden = builder.hasGarden;
        this.hasSwimmingPool = builder.hasSwimmingPool;
    }
}

// Builder Class cho House
class HouseBuilder {
    public floors: number;
    public hasGarden: boolean;
    public hasSwimmingPool: boolean;
    constructor() {
        this.floors = 1;
        this.hasGarden = false;
        this.hasSwimmingPool = false;
    }
    public setFloors(floors: number): HouseBuilder {
        this.floors = floors; return this;
    }
    public setGarden(hasGarden: boolean): HouseBuilder {
        this.hasGarden = hasGarden; return this;
    }
    public setSwimmingPool(hasSwimmingPool: boolean): HouseBuilder {
        this.hasSwimmingPool = hasSwimmingPool; return this;
    }
    public build(): House {
        return new House(this);
    }
}
// Sử dụng Builder để tạo đối tượng House
const house = new HouseBuilder()
    .setFloors(2)
    .setGarden(true)
    .setSwimmingPool(false)
    .build();

```

Lợi ích
- Tạo đối tượng phức tạp: Builder Pattern cho phép bạn tạo các đối tượng phức tạp một cách linh hoạt mà không cần phải sử dụng quá nhiều tham số trong constructor.
- Dễ mở rộng: Bạn có thể dễ dàng thêm các thuộc tính mới vào House mà không cần thay đổi cấu trúc hiện tại.
- Đọc mã dễ dàng hơn: Cách gọi chuỗi các phương thức giúp mã dễ đọc và duy trì hơn.


### `5. Prototype` 
Prototype Pattern cung cấp cơ chế để copy từ object ban đầu sang object mới và thay đổi giá trị một số thuộc tính nếu cần.

## Structural Patterns:
là một tập hợp các mẫu thiết kế tập trung vào việc tổ chức và kết hợp các class và object để tạo thành các cấu trúc lớn hơn. Các mẫu này nhằm mục đích nâng cao tính linh hoạt, khả năng sử dụng lại và khả năng bảo trì của code bằng cách thúc đẩy sự cộng tác giữa class và object. Dưới đây là chi tiết các mẫu trong nhóm structural:
### `6. Adapter`
Mẫu này được sử dụng để chuyển đổi giao diện, giúp hai bên có thể làm việc cùng nhau thông qua giao diện trung gian, không cần thay đổi code của lớp có sẵn cũng như class đang viết.

Giả sử bạn đang làm việc với một hệ thống quản lý người dùng cũ có lớp OldUserManager với các phương thức khác với lớp NewUserManager mà bạn muốn sử dụng. Bạn muốn tích hợp lớp mới vào hệ thống mà không thay đổi mã của lớp cũ.

```typescript
interface NewUserManager {
    addUser(name: string): void;
    removeUser(name: string): void;
}

class OldUserManager {
    public createUser(userName: string): void {
        console.log(`User ${userName} created.`);
    }

    public deleteUser(userName: string): void {
        console.log(`User ${userName} deleted.`);
    }
}

class UserManagerAdapter implements NewUserManager {
    private oldUserManager: OldUserManager;

    constructor(oldUserManager: OldUserManager) {
        this.oldUserManager = oldUserManager;
    }

    public addUser(name: string): void {
        this.oldUserManager.createUser(name);
    }

    public removeUser(name: string): void {
        this.oldUserManager.deleteUser(name);
    }
}

// Client Code: Sử dụng giao diện NewUserManager
function manageUsers(userManager: NewUserManager) {
    userManager.addUser("Alice");
    userManager.removeUser("Bob");
}

// Sử dụng Adapter Pattern
const oldUserManager = new OldUserManager();
const adaptedUserManager = new UserManagerAdapter(oldUserManager);

manageUsers(adaptedUserManager);
// Output:
// User Alice created.
// User Bob deleted.
```
Lợi ích:
- Tích hợp hệ thống cũ: Adapter Pattern cho phép tích hợp các hệ thống hoặc thư viện cũ mà không cần thay đổi mã nguồn của chúng.
- Tách biệt hệ thống: Giúp tách biệt các hệ thống hoặc thư viện khác nhau, làm cho mã dễ bảo trì và mở rộng hơn.
- Khả năng mở rộng: Bạn có thể dễ dàng thêm hoặc thay đổi các lớp mới mà không cần thay đổi mã của các lớp hiện có hoặc mã client.
- Dễ sử dụng: Đảm bảo rằng các lớp có giao diện không tương thích có thể làm việc cùng nhau mà không cần phải sửa đổi mã của chúng.

### `7. Bridge`
Bridge là một mẫu thiết kế cấu trúc cho phép bạn chia một class lớn hoặc một tập hợp các class có liên quan chặt chẽ thành hai hệ thống phân cấp riêng biệt là trừu tượng hóa (abstraction) và  tính hiện thực (implementation).

### `8. Composite`
Mẫu Composite cho phép khách hàng xử lý các collection object và các object riêng lẻ một cách thống nhất. Một cách để xác định mẫu Composite là cấu trúc dạng cây.

### `9. Decorator`
Đây là một mẫu thiết kế cấu trúc cho phép bạn đính kèm các hành vi mới vào các object, bằng cách đặt các object này bên trong các object khác, được bao bọc đặc biệt có chứa các hành vi đó.

```typescript
// Interface Report định nghĩa các phương thức cơ bản
interface Report {
    generate(): string;
}
class BasicReport implements Report {
    public generate(): string { return "Basic Report"; }
}
abstract class ReportDecorator implements Report {
    protected report: Report;
    constructor(report: Report) {
        this.report = report;
    }
    public generate(): string { return this.report.generate(); }
}
class PDFDecorator extends ReportDecorator {
    public generate(): string { return `${super.generate()} (PDF Format)`; }
}
class EmailDecorator extends ReportDecorator {
    public generate(): string { return `${super.generate()} (Sent via Email)`;}
}
// Sử dụng các decorators để tạo một báo cáo với các tính năng mở rộng
const basicReport = new BasicReport(); console.log(basicReport.generate()); // Output: Basic Report

const pdfReport = new PDFDecorator(basicReport); console.log(pdfReport.generate()); // Output: Basic Report (PDF Format)

const emailReport = new EmailDecorator(pdfReport); console.log(emailReport.generate()); // Output: Basic Report (PDF Format) (Sent via Email)
```
Lợi ích:
- Tính linh hoạt: Bạn có thể kết hợp nhiều decorator để tùy chỉnh báo cáo theo nhu cầu mà không cần phải thay đổi lớp BasicReport.
- Mở rộng dễ dàng: Nếu cần thêm tính năng mới, bạn chỉ cần tạo lớp decorator mới mà không ảnh hưởng đến lớp cơ bản hoặc các decorator hiện có.
- Bảo trì dễ dàng: Mỗi decorator có trách nhiệm cụ thể, giúp mã dễ bảo trì và mở rộng hơn.

### `10. Facade`
Công việc duy nhất của mẫu thiết kế Facade là làm cho giao diện sử dụng đơn giản hơn. Nó được sử dụng để đơn giản hóa giao diện của một hoặc nhiều class để dễ sử dụng hơn.

### `11. Flyweight`
Flyweight là một mẫu thiết kế cấu trúc cho phép bạn đưa nhiều object hơn vào lượng RAM có sẵn, bằng cách chia sẻ các phần trạng thái chung giữa nhiều object thay vì giữ tất cả dữ liệu trong từng object.

### `12. Proxy`
Proxy là một mẫu thiết kế cấu trúc cho phép bạn kiểm soát quyền truy cập của một đối tượng vì nhiều lý do khác nhau, ví dụ như Bảo mật, Hiệu suất, Bộ đệm, v.v.. Proxy giúp kiểm soát quyền truy cập vào đối tượng ban đầu, cho phép bạn thực hiện điều gì đó trước hoặc sau khi yêu cầu được chuyển đến đối tượng đó

## Behavioral Patterns:
là một tập hợp các mẫu thiết kế tập trung vào việc xác định giao tiếp và tương tác giữa các object và class. Các mẫu này thúc đẩy tính linh hoạt, khả năng sử dụng lại và khả năng bảo trì bằng cách gói gọn các hành vi khác nhau trong các object riêng biệt.

### `13. Chain of Responsibility`
Đây là một mẫu thiết kế hành vi cho phép bạn chuyển các request dọc theo một chuỗi handler. Khi nhận được request, mỗi handler sẽ quyết định xử lý yêu cầu hoặc chuyển nó cho handler tiếp theo trong chuỗi.

### `14. Command`
Command là một mẫu thiết kế hành vi biến request thành một object độc lập chứa tất cả thông tin về request. Việc chuyển đổi này cho phép bạn chuyển các request dưới dạng phương thức arguments, delay hoặc queue để thực thi request và hỗ trợ các hoạt động không thể hoàn tác.

Người request chỉ biết về Command object và không biết chi tiết cụ thể về object thực tế, điều này làm giảm sự kết hợp giữa người request và đối tượng hành động.

Tất cả những gì người request cần biết là phương thức gọi trên command object, sau đó ủy quyền request cho đối tượng hành động cụ thể. 

```typescript
interface Command {
    execute(): void;
}
// Concrete Command: Lệnh bật thiết bị
class TurnOnCommand implements Command {
    private device: Device;
    constructor(device: Device) {
        this.device = device;
    }
    public execute(): void {this.device.turnOn(); }
}
// Concrete Command: Lệnh tắt thiết bị
class TurnOffCommand implements Command {
    private device: Device;
    constructor(device: Device) {
        this.device = device;
    }
    public execute(): void { this.device.turnOff();}
}
// Concrete Command: Lệnh điều chỉnh âm lượng
class VolumeUpCommand implements Command {
    private device: Device;
    constructor(device: Device) {
        this.device = device;
    }
    public execute(): void {this.device.volumeUp();}
}
// Receiver: Thiết bị điện tử cụ thể
class Device {
    public turnOn(): void {console.log("Device is turned on");}
    public turnOff(): void { console.log("Device is turned off");}
    public volumeUp(): void {console.log("Volume is increased");}
}
// Invoker: Điều khiển từ xa
class RemoteControl {
    private command: Command;
    public setCommand(command: Command): void { this.command = command;}
    public pressButton(): void { this.command.execute();}
}

// Sử dụng Command Pattern
const device = new Device();

const turnOn = new TurnOnCommand(device);
const turnOff = new TurnOffCommand(device);
const volumeUp = new VolumeUpCommand(device);

const remoteControl = new RemoteControl();

remoteControl.setCommand(turnOn);
remoteControl.pressButton(); // Output: Device is turned on

remoteControl.setCommand(volumeUp);
remoteControl.pressButton(); // Output: Volume is increased

remoteControl.setCommand(turnOff);
remoteControl.pressButton(); // Output: Device is turned off
```

Lợi ích:
- Tách biệt việc yêu cầu và thực hiện hành động: Command Pattern giúp tách biệt yêu cầu thực hiện hành động từ việc thực hiện hành động đó, giúp mã nguồn trở nên sạch sẽ và dễ bảo trì hơn.
- Dễ dàng thêm các lệnh mới: Bạn có thể thêm các lệnh mới mà không cần thay đổi các lớp hiện có. Điều này giúp mở rộng hệ thống một cách dễ dàng.
- Hỗ trợ undo/redo: Bạn có thể dễ dàng lưu trữ và hủy các lệnh hoặc lặp lại các lệnh nếu cần.
- Quản lý lịch sử lệnh: Bạn có thể lưu trữ lịch sử các lệnh để xử lý các tính năng như undo hoặc redo.

### `15. Interpreter`
Đây là một mẫu hành vi giúp ích cho việc tạo trình thông dịch ngôn ngữ. Nó cho phép diễn giải một ngôn ngữ hoặc biểu thức nhất định bằng cách xác định ngữ pháp của nó và cung cấp trình thông dịch để đánh giá và thực hiện các biểu thức.

Interpreter thúc đẩy khả năng mở rộng và bảo trì bằng cách tách language-specific logic khỏi phần còn lại của ứng dụng, giúp việc giới thiệu các tính năng hoặc biến thể ngôn ngữ mới dễ dàng hơn.

### `16. Iterator`
Iterator là một mẫu thiết kế hành vi cho phép bạn duyệt qua các phần tử của một collection mà không cần phải hiểu rõ về những chi tiết bên trong của những tập hợp này. (list, stack, tree, v.v.).

Mẫu này giúp thúc đẩy khả năng sử dụng lại code, đơn giản hóa việc truyền tải collection và tăng cường khả năng bảo trì bằng cách tách biệt các vấn đề lặp lại khỏi chức năng cốt lõi.

### `17. Mediator`
Mediator là một mẫu hành vi tạo điều kiện thuận lợi cho việc giao tiếp giữa nhiều object mà không cần dependency trực tiếp. Nó thúc đẩy sự ghép nối lỏng lẻo (loose coupling) bằng cách mang đến một bộ mediator hoạt động như một trung tâm liên lạc.

### `18. Memento`
Memento là một mẫu thiết kế cho phép bạn lưu và khôi phục trạng thái trước đó của một object mà không tiết lộ chi tiết về việc triển khai nó. Mẫy này giúp ích trong việc đóng gói dữ liệu và duy trì tính toàn vẹn của object, vì trạng thái vẫn bị ẩn khỏi truy cập từ bên ngoài.

### `19. Observer`
Observer là một mẫu thiết kế hành vi cho phép bạn xác định cơ chế đăng ký để thông báo cho nhiều object về bất kỳ sự kiện nào xảy ra với object mà chúng đang quan sát.

```typescript
// Observer Interface định nghĩa phương thức nhận thông báo khi có sự thay đổi
interface Observer {
    update(stockPrice: number): void;
}
// Subject Interface định nghĩa các phương thức thêm, xóa observers và thông báo
interface Subject {
    addObserver(observer: Observer): void;
    removeObserver(observer: Observer): void;
    notifyObservers(): void;
}
// Concrete Observer: Nhà đầu tư cụ thể nhận thông báo
class Investor implements Observer {
    private name: string;
    constructor(name: string) {
        this.name = name;
    }
    public update(stockPrice: number): void { console.log(`${this.name} nhận được thông báo: Giá chứng khoán hiện tại là $${stockPrice}`);}
}

// Concrete Subject: Chứng khoán cụ thể
class Stock implements Subject {
    private observers: Observer[] = [];
    private price: number = 0;
    public addObserver(observer: Observer): void {
        this.observers.push(observer);
    }
    public removeObserver(observer: Observer): void {
        this.observers = this.observers.filter(obs => obs !== observer);
    }
    public notifyObservers(): void {
        for (const observer of this.observers) {
            observer.update(this.price);
        }
    }
    public setPrice(price: number): void {
        this.price = price;
        this.notifyObservers();
    }
}
// Sử dụng Observer Pattern
const stock = new Stock();
const investor1 = new Investor('Nhà đầu tư A');
const investor2 = new Investor('Nhà đầu tư B');
stock.addObserver(investor1);
stock.addObserver(investor2);
stock.setPrice(100); // Thay đổi giá chứng khoán và thông báo cho các nhà đầu tư
stock.setPrice(150); // Thay đổi giá chứng khoán và thông báo cho các nhà đầu tư
// Output:
// Nhà đầu tư A nhận được thông báo: Giá chứng khoán hiện tại là $100
// Nhà đầu tư B nhận được thông báo: Giá chứng khoán hiện tại là $100
// Nhà đầu tư A nhận được thông báo: Giá chứng khoán hiện tại là $150
// Nhà đầu tư B nhận được thông báo: Giá chứng khoán hiện tại là $150
```
Lợi ích:
- Giảm kết nối giữa các đối tượng: Stock không cần biết chi tiết về các Investor, nó chỉ cần thông báo khi có sự thay đổi. Điều này giúp giảm sự phụ thuộc giữa các đối tượng.
- Dễ mở rộng: Bạn có thể dễ dàng thêm hoặc xóa các observers mà không cần thay đổi mã của Stock hoặc các observers khác.
- Tính linh hoạt: Cho phép nhiều đối tượng (observers) cùng theo dõi và phản ứng với sự thay đổi của một đối tượng (subject) mà không cần phải quản lý chúng theo cách thủ công.


### `20. State`
State Pattern là một mẫu thiết kế hành vi cho phép một object thay đổi hành vi của nó khi trạng thái bên trong của nó thay đổi. 

### `21. Strategy`
Strategy là một mẫu thiết kế hành vi cho phép bạn xác định một nhóm thuật toán, đặt mỗi thuật toán vào một class riêng biệt và làm cho các object của chúng có thể hoán đổi cho nhau.

Mẫu này dựa trên nguyên tắc Open Closed design nhằm thúc đẩy cách viết code có thể mở rộng mà không cần chạm vào code đã được thử và kiểm tra.

### `22. Template Method`
Đây là một mẫu thiết kế hành vi xác định framework của thuật toán trong lớp cha (Superclasses) nhưng cho phép các lớp con (sub class) ghi đè các bước cụ thể của thuật toán mà không thay đổi cấu trúc của nó.
```typescript
abstract class DataProcessingTemplate {
    public processFile(filePath: string): void {
        this.initialize();
        const rawData = this.readFile(filePath);
        const data = this.parseData(rawData);
        this.processData(data);
        this.finalize();
    }

    // Các phương thức có thể thay đổi
    protected abstract readFile(filePath: string): string;
    protected abstract parseData(data: string): any;
    protected abstract processData(data: any): void;

    private initialize(): void { console.log("Initialization..."); }

    private finalize(): void { console.log("Finalization..."); }
}

// Concrete Class: Xử lý dữ liệu từ file CSV
class CsvDataProcessor extends DataProcessingTemplate {
    protected readFile(filePath: string): string {
        console.log(`Reading CSV file from ${filePath}`);
        return "name,age\nAlice,30\nBob,25";
    }

    protected parseData(data: string): any {
        console.log("Parsing CSV data...");
        return data.split('\n').slice(1).map(line => {
            const [name, age] = line.split(',');
            return { name, age: parseInt(age) };
        });
    }

    protected processData(data: any): void { console.log("Processing CSV data:", data); }
}

// Concrete Class: Xử lý dữ liệu từ file JSON
class JsonDataProcessor extends DataProcessingTemplate {
    protected readFile(filePath: string): string {
        console.log(`Reading JSON file from ${filePath}`);
        return '{"employees": [{"name": "Alice", "age": 30}, {"name": "Bob", "age": 25}]}';
    }

    protected parseData(data: string): any {
        console.log("Parsing JSON data...");
        return JSON.parse(data).employees;
    }

    protected processData(data: any): void {
        console.log("Processing JSON data:", data);
    }
}
const csvProcessor = new CsvDataProcessor();
csvProcessor.processFile("path/to/data.csv");

const jsonProcessor = new JsonDataProcessor();
jsonProcessor.processFile("path/to/data.json");
```
Lợi ích:
- Tái sử dụng mã: Cấu trúc chung của quá trình import được định nghĩa trong lớp cơ sở, giúp giảm thiểu mã trùng lặp.
- Dễ bảo trì: Giữ cho phần cấu trúc chung không thay đổi và chỉ thay đổi các bước cụ thể trong các lớp con.
- Khả năng mở rộng: Dễ dàng thêm các loại file mới mà không cần thay đổi mã của lớp cơ sở.
- Tính linh hoạt: Cho phép các lớp con cung cấp các cách thực hiện khác nhau cho các bước cụ thể của quá trình import dữ liệu.

### `23. Visitor`
Visitor là một mẫu thiết kế hành vi cho phép bạn tách biệt các thuật toán khỏi các object mà chúng hoạt động trên đó.