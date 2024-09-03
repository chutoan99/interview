### Phân biệt Call, Apply, Bind:

| Call | Apply | Bind |
|------|-------|------|
| `call` gọi hàm trực tiếp và truyền các tham số vào lần lượt. | `apply` cũng gọi hàm trực tiếp nhưng truyền các tham số trong một mảng. | `bind` không gọi hàm ngay lập tức mà trả về một hàm mới với `this` đã được gán cố định và có thể truyền trước một số tham số. | 

`Call`
```typescript  
var person1 = {firstName: 'Khoa', lastName: 'Nguyễn'};
var person2 = {firstName: 'Vân', lastName: 'Thanh'};

function say(greeting1, greeting2) {
 console.log(greeting1 + ',' + greeting2 + ' ' + this.firstName + ' ' + this.lastName);
}

say.call(person1, 'Hello', 'Good morning'); // => Hello,Good morning Khoa Nguyen
say.call(person2, 'Hello', 'Good morning'); // => Hello,Good morning Vân Thanh
``` 

`Apply`

```typescript  
var person1 = {firstName: 'Khoa', lastName: 'Nguyễn'};
var person2 = {firstName: 'Vân', lastName: 'Thanh'};

function say(greeting0, greeting1) {
 console.log(greeting0 + ',' + greeting1 + ' ' + this.firstName + ' ' + this.lastName);
}

say.apply(person1, ['Hello', 'Good moring']); // => Hello,Good moring Khoa Nguyễn
say.apply(person2, ['Hello', 'Good moring']); // => Hello,Good moring Vân Thanh
``` 

`Bind`
```typescript  
var person1 = {firstName: 'Khoa', lastName: 'Nguyễn'};
var person2 = {firstName: 'Vân', lastName: 'Thanh'};

function say(greeting0, greeting1) {
 console.log(greeting0 + ',' + greeting1 + ' ' + this.firstName + ' ' + this.lastName);
}

var sayHelloKhoa = say.bind(person1, 'Hello', 'Good morning');
var sayHelloVan = say.bind(person2, 'Hello', 'Good morning');

sayHelloKhoa(); // => Hello,Good morning Khoa Nguyễn
sayHelloVan(); // => Hello,Good morning Vân Thanh
``` 

- Nhìn chung, hàm call và apply là gần giống nhau. Chúng đều gọi hàm trực tiếp. Chỉ khác ở cách truyền tham số vào (apply truyền vào một array chứa toàn bộ các tham số còn call truyền lần lượt từng tham số.)

- Hàm bind thì hơi khác hơn một chút. Hàm này không gọi hàm trực tiếp mà nó sẽ trả về một hàm mới. Và bạn có thể sử dụng hàm số mới này sau. Về cách truyền tham số vào thì nó giống với hàm call.

### Closures 
 Closures xảy ra khi một hàm "nhớ" được phạm vi (scope) mà nó được khai báo, ngay cả khi hàm đó được thực thi ngoài phạm vi ban đầu của nó.
Closures cho phép một hàm truy cập vào biến của phạm vi bên ngoài ngay cả sau khi phạm vi bên ngoài đã kết thúc.

```typescript
function outerFunction() {
    let outerVariable = "I am from outer scope";
    function innerFunction() { console.log(outerVariable); // Sử dụng biến từ phạm vi bên ngoài }
    return innerFunction;
}
const closureFunc = outerFunction();
closureFunc(); // "I am from outer scope"
```

### Event loop trong javascript
![My Image](https://www.loginradius.com/blog/static/68b5a28f6bdca97b73593056ae425a8d/e5715/event_loop_illustration.png)


Ban dầu các tác vụ khi mà thực thi thì sẽ năm ở trong call tasck, 
Vd
- khi mà thực hiện làm log(1) thì nó kiểm tra đây có phải hàm thực thi các tác vụ bất độ hay không, nếu không thì nó sẽ thực thin gay và xóa nó khỏi call stask
- khi gặp 1 hàm chờ 2s thì nó sẽ chuyển hàm có vào webApi, webapi sẽ đợi 2s, và chuyển hàm đó thành call back và chuyển nó vào hang đợi, 
- event loop sẽ kiểm tra các hàm trong call stask xem còn hàm nào hay không, nếu không thì nó sẽ chuyển hàm call back đang Queue sang call task và thực thi nó, vòng đời nó cứ như vậy
Ngoài ra thì Queue nó lại chi làm 2 thành phần là Micro Task Queue vs Macro Task Queue
  Macro Task: Tác vụ không đồng bộ như setTimeout, setInterval, hoặc I/O operation sẽ được đẩy vào macro task queue. Khi call stack trống, event loop sẽ thực thi tất cả các micro task trước.
  Micro Task: Tác vụ như Promise.resolve().then() hoặc process.nextTick sẽ được đẩy vào micro task queue.
Sau khi micro task queue trống, event loop sẽ thực thi một macro task.
