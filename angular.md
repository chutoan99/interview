### 1. Vòng đời của Components trong Angular

![My Image](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRYSZTzRzPOZFUROXL4jK6hSMwBJulk-Ce7XQ&s)

`- contructor:` phương thức khởi tạo của class, dùng để khai báo các dependenciew jnjectiong của comoponnet, hạn chế việc logic vào contructor
`- ngOnChanges:` nó sẽ thực thi khi mà phát hiện sự thay đổi của các input dầu vào: thường được cập nhất các giá trị inpout đầu vào
`- ngOnInit:` chạy ngay sau ngonchanges, thường được dùng để gọi api
`- ngDoCheck :` chạy lần đầu tiên sau ngOnit và mỗi khi phát hiện sự thay đổi của change detection chạy
`- ngAfterContentInit:` thực thi khi mà angular chiếu các content vào phần view componet, thông qua thể ng-content. chạy duy nhất 1 lần sau khi ngDocheck,.
`- ngAfterContentChecked:` chay sau khi angular kiểm tra các content đã truyền vào component, phương thức này gọi lần đầu khi ngAfterContentInit chạy và sau mỗi lần `- ngDoCheck chạy từ lần thứ 2 trở đi
` - ngAfterViewInit:` chạy khi component đã hoàn thành khởi tạo xong các thành phần view và view con, thường được dùng để tham chiếu đến các component thông qua ViewChild và Viewchildren.
`- ngAfterViewChecked:` được gọi sau khi sau khi angular đã kiểm tra các thành phần view và view con, được gọi sau ngAfterViewInit và mỗi lần ngAfterContentChecked chạy.
`- ngDeTroy:` được gọi khi component bị phá hủy. Thường được dùng để handel các tác vụ unsubrice

