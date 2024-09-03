# 1 CLASS:
## Các thuộc tính khai báo trong class 
    - protected: Thuộc tính có thể được truy cập từ bên trong lớp và các lớp con (subclass).
    - private: chỉ có thể được truy cập từ bên trong lớp.
    - public: Thuộc tính có thể được truy cập từ bất kỳ đâu.
    - static: các thuộc tính không cần phải khởi tạo
    - readonly: các thuộc tính bên trong không thể bị thay đổi khi khởi tạo
    - abstract: không được khai báo trực tiếp trong lớp mà trong các lớp trừu tượng (abstract class). 

# 2 DECORATOR: Cho phép bạn thêm metadata hoặc thay đổi hành vi của các lớp, phương thức, thuộc tính, hoặc tham số. 

## 1. Class Decorators:
```typescript
function LogClass(target: Function) { console.log(`Class ${target.name} is being created`);}
@LogClass
class MyClass {
  constructor(public name: string) {}
}
const obj = new MyClass('Decorator Example'); // Console: Class MyClass is being created
```

## 2. Method Decorators
```typescript
function LogMethod(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;
  descriptor.value = function (...args: any[]) {
    console.log(`Method ${propertyKey} called with arguments: ${args}`);
    return originalMethod.apply(this, args);
  };
}
class MyClass {
  @LogMethod
  myMethod(arg: number) { console.log(`Original method logic with argument: ${arg}`); }
}
const obj = new MyClass();
obj.myMethod(42); 
// Console: Method myMethod called with arguments: 42 
// Console: Original method logic with argument: 42
```

## 3. Property Decorators
```typescript
function LogProperty(target: any, propertyKey: string) {
  let value = target[propertyKey];
  const getter = () => { 
    console.log(`Get value of ${propertyKey}: ${value}`); 
    return value;
    };
  const setter = (newValue: any) => {
    console.log(`Set value of ${propertyKey} to: ${newValue}`);
    value = newValue;
    };
  Object.defineProperty(target, propertyKey, {
    get: getter,
    set: setter,
    enumerable: true,
    configurable: true
  });
}

class MyClass {
  @LogProperty
  myProp: string;
  constructor(value: string) {
    this.myProp = value;
  }
}

const obj = new MyClass('Initial Value');
obj.myProp = 'New Value';
// Console: Set value of myProp to: New Value
// Console: Get value of myProp: New Value
```

## 4. Parameter Decorators
```typescript
function LogParameter(target: any, propertyKey: string, parameterIndex: number) {
  console.log(`Parameter at index ${parameterIndex} in method ${propertyKey} is decorated`);
}
class MyClass {
  myMethod(@LogParameter param: number) {
    console.log(`Parameter value: ${param}`);
  }
}
const obj = new MyClass();
obj.myMethod(42);
// Console: Parameter at index 0 in method myMethod is decorated
// Console: Parameter value: 42
```

# 3 ENUM: Cho phép định nghĩa một tập hợp các hằng số có tên
```typescript
enum Direction {
  Up,    // 0
  Down,  // 1
  Left,  // 2
  Right  // 3
}
```

# 4 OOP: 
## Encapsulation (Đóng gói): Sử dụng access modifiers (public, private, protected) để giới hạn quyền truy cập của các thuộc tính , methods của class
## Inheritance (kế thừa): Sử dụng từ khóa 'extends' để kế thừa thuộc tính và phương thức từ lớp cha.
## Polymorphism (Đa hình): phương thức ghi đè (method overriding) Cho phép một phương thức có thể hoạt động khác nhau tùy vào đối tượng gọi nó
## Abstraction (Trừu tượng): các phương thức mà các lớp con phải triển khai, thông qua abstract class hoặc interface.

# 5 Namespace && Module: 
Namespace là cách tổ chức mã trong một không gian tên chung trong cùng một hoặc một nhóm tệp. Nó không hỗ trợ các tính năng của hệ thống module hiện đại.

Module (ES6 modules) là cách phân chia mã thành các tệp riêng biệt với cơ chế export và import, hỗ trợ tốt hơn cho việc quản lý mã nguồn trong các dự án lớn và hiện đại.

# 6 UTILITY TYPES:

## 1 Awaited<Type>: Trích xuất loại giá trị mà một Promise sẽ trả về
```typescript
async function fetchData(): Promise<number> {
    return 42;
  }
type ResultType = Awaited<ReturnType<typeof fetchData>>; //* ResultType sẽ là number
```

## 2 Partial<Type>: Biến các thuộc tính trong 1 đối tượng thành optional
```typescript
interface User {
  id: number;
  name: string;
}
type PartialUser = Partial<User>;

const updateUser: PartialUser = {
  name: "John Doe",
};
```

## 3 Required<Type>: Biến các thuộc tính trong 1 đối tượng thành bắt buộc
```typescript
interface User {
  id: number;
  name?: string;
}
type RequiredUser = Required<User>;

const user: RequiredUser = {
  id: 1,
  name: "Alice",
};
```

## 4 Readonly<Type>: Biến các thuộc tính trong 1 đối tượng thành chỉ đọc
```typescript
interface User {
  id: number;
  name?: string;
}

const user: Readonly<User> = {
  id: 1,
  name: "Alice",
};

// Cố gắng thay đổi thuộc tính sẽ gây ra lỗi
user.name = "Bob"; // Error: Cannot assign to 'name' because it is a read-only property.
```

## 5 Record<Keys, Type>: Cho phép bạn chỉ định một tập hợp các khóa và kiểu dữ liệu cho các giá trị tương ứng với các khóa đó.
```typescript
enum Color {
  Red = "RED",
  Green = "GREEN"
}

const colorDescriptions: Record<Color, string> = {
  [Color.Red]: "A bright and warm color.",
  [Color.Green]: "The color of nature.",
};
```

## 6 Pick<Type, Keys>: Tạo một loại mới từ một loại (Type) hiện tại chỉ với các thuộc tính(Keys) được "chỉ định".
```typescript
interface User {
  id: number;
  name: string;
  email: string;
  age: number;
}
//* tạo ra 1 đối tượng mới (gồm các keys là 'id' và 'name') từ User
type UserSummary = Pick<User, 'id' | 'name'>;

const userSummary: UserSummary = {
  id: 1,
  name: "Alice"
};
```

## 7 Omit<Type, Keys>: Tạo một loại mới từ một loại (type) hiện tại bằng cách "loại bỏ" một hoặc nhiều thuộc tính cụ thể.

```typescript
interface User {
  id: number;
  name: string;
  email: string;
  age: number;
}
//* tạo ra 1 đối tượng mới bằng cách loại bỏ (gồm các keys là 'id' và 'name') từ User
type UserSummary = Omit<User, 'id' | 'name'>;

const userSummary: UserSummary = {
  email: 'struongvanchutoan1999@gmail.com',
  age: 15
};
```

## 8 Exclude<Type, Union>: Loại bỏ các loại thuộc U khỏi một tập hợp loại T.

```typescript
type AllTypes = 'a' | 'b' | 'c' | 'd';
type ExcludedTypes = 'b' | 'd';
// Loại bỏ các kiểu trong ExcludedTypes khỏi AllTypes
type Result = Exclude<AllTypes, ExcludedTypes>; // Kết quả: 'a' | 'c'
```

## 9 Extract<Type, Union>:  Lấy các kiểu thuộc T mà cũng thuộc U.
```typescript
type A = 'a' | 'b' | 'c';
type B = 'b' | 'c' | 'd';

// Lấy các kiểu từ A mà cũng xuất hiện trong B
type Result = Extract<A, B>; // Kết quả: 'b' | 'c'
```

## 10 NonNullable<Type>: Loại bỏ các kiểu null và undefined khỏi một tập hợp kiểu.
```typescript
type NullableString = string | null | undefined;

// Loại bỏ null và undefined
type NonNullableString = NonNullable<NullableString>; // Kết quả: string

```

## 11 Parameters<Type>: Trích xuất các tham số của một hàm từ kiểu hàm T và tạo ra một tuple (mảng) chứa các loại của các tham số đó
```typescript
function add(a: number, b: number): number {
  return a + b;
}
// Trích xuất các tham số của hàm `add`
type AddParameters = Parameters<typeof add>; // Kết quả: [number, number]
```

## 12 ConstructorParameters<Type>: Trích xuất các tham số của một hàm constructor từ một kiểu lớp hoặc kiểu constructor function
```typescript
class Person {
  constructor(public name: string, public age: number) {}
}

// Trích xuất các tham số của constructor từ lớp `Person`
type PersonConstructorParams = ConstructorParameters<typeof Person>; // Kết quả: [string, number]
```

## 13 ReturnType<Type>: Trích xuất kết quả trả về của 1 hàm
```typescript
function getUserInfo(userId: number): { name: string; age: number } {
  return { name: 'Alice', age: 30 };
}

type UserInfo = ReturnType<typeof getUserInfo>; // Kết quả: { name: string; age: number }
```

## 14 InstanceType<Type>: lấy kiểu của thể hiện (instance) của một lớp hoặc một hàm constructor từ một kiểu lớp hoặc hàm constructor. 
```typescript
class Person {
  constructor(public name: string, public age: number) {}
}

// Trích xuất kiểu thể hiện của lớp `Person`
type PersonInstance = InstanceType<typeof Person>; // Kết quả: Person
```

## 15 ThisParameterType<Type>: Lấy kiểu của tham số 'this' từ một hàm hoặc một phương thức trong lớp
```typescript
class Person {
  name: string;
  age: number;
  constructor(name: string, age: number) {
    this.name = name; this.age = age;
  }
  greet(this: Person): string {
    return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
  }
}
// Trích xuất kiểu tham số `this` của phương thức `greet`
type GreetThisType = ThisParameterType<typeof Person.prototype.greet>; // Kết quả: Person
```

## 16 OmitThisParameter<Type>: Loại bỏ tham số this khỏi kiểu hàm.
```typescript
function example(this: { name: string }, age: number): void {}

// Loại bỏ tham số `this`
type ExampleWithoutThis = OmitThisParameter<typeof example>;
// Kiểu của ExampleWithoutThis sẽ là (age: number) => void
const exampleFunction: ExampleWithoutThis = (age) => {};
```

## 17 ThisType<Type>: Cung cấp thông tin về loại của this trong một đối tượng.
```typescript
interface Person {
  name: string;
  greet(): void;
}
// Đối tượng với phương thức sử dụng kiểu `this`
const personPrototype: ThisType<Person> = {
  name: "Alice",
  greet(this: Person) {
    console.log(`Hello, ${this.name}`);
  },
};
// Tạo một đối tượng từ prototype
const person = Object.create(personPrototype);
person.name = "Bob";
person.greet(); // Output: Hello, Bob
```

