### Phân biệt Call, Apply, Bind:

### Phân biệt Call, Apply, Bind

### Phân biệt Call, Apply, Bind

| Call | Apply | Bind |
|------|-------|------|
| `call` gọi hàm trực tiếp và truyền các tham số vào lần lượt. | `apply` cũng gọi hàm trực tiếp nhưng truyền các tham số trong một mảng. | `bind` không gọi hàm ngay lập tức mà trả về một hàm mới với `this` đã được gán cố định và có thể truyền trước một số tham số. |
| ```typescript  var person1 = {firstName: 'Khoa', lastName: 'Nguyễn'}; var person2 = {firstName: 'Vân', lastName: 'Thanh'}; function say(greeting1, greeting2) { console.log(greeting1 + ',' + greeting2 + ' ' + this.firstName + ' ' + this.lastName); } say.call(person1, 'Hello', 'Good morning'); // => Hello,Good morning Khoa Nguyễn say.call(person2, 'Hello', 'Good morning'); // => Hello,Good morning Vân Thanh ``` | ```typescript var person1 = {firstName: 'Khoa', lastName: 'Nguyễn'}; var person2 = {firstName: 'Vân', lastName: 'Thanh'}; function say(greeting0, greeting1) { console.log(greeting0 + ',' + greeting1 + ' ' + this.firstName + ' ' + this.lastName); } say.apply(person1, ['Hello', 'Good morning']); // => Hello,Good morning Khoa Nguyễn say.apply(person2, ['Hello', 'Good morning']); // => Hello,Good morning Vân Thanh ``` | ```typescript var person1 = {firstName: 'Khoa', lastName: 'Nguyễn'}; var person2 = {firstName: 'Vân', lastName: 'Thanh'}; function say(greeting0, greeting1) { console.log(greeting0 + ',' + greeting1 + ' ' + this.firstName + ' ' + this.lastName); } var sayHelloKhoa = say.bind(person1, 'Hello', 'Good morning'); var sayHelloVan = say.bind(person2, 'Hello', 'Good morning'); sayHelloKhoa(); // => Hello,Good morning Khoa Nguyễn sayHelloVan(); // => Hello,Good morning Vân Thanh ``` |


Sau khi xem qua 3 ví dụ sau, chúng ta có thể rút ra 1 vài nhận xét:
- Nhìn chung, hàm call và apply là gần giống nhau. Chúng đều gọi hàm trực tiếp. Chỉ khác ở cách truyền tham số vào (apply truyền vào một array chứa toàn bộ các tham số còn call truyền lần lượt từng tham số.)

- Hàm bind thì hơi khác hơn một chút. Hàm này không gọi hàm trực tiếp mà nó sẽ trả về một hàm mới. Và bạn có thể sử dụng hàm số mới này sau. Về cách truyền tham số vào thì nó giống với hàm call.
