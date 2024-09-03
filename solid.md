# SOLID:

## Single responsibility principle (SRP): Nguyên tắc trách nhiệm đơn nhất:
Một class chịu trách một việc mà thôi
## Open/close principle (OCP): Nguyên tắc mở/đóng:
Chỉ nên mở rộng một class bằng cách kế thừa. Tuyệt đối không mở rộng
class bằng cách sửa đổi nó.
## Liskov substitution principle (LSP): Nguyên tắc thay thế Liskov:
Trong một chương trình, các object của class con có thể thay thế class cha 
mà không làm thay đổi tính đúng đắn của chương trình
## Interface segregation principle (ISP): Nguyên tắc phân chia interface:
Nên tách Interface thành nhiều interface nhỏ với những mục đích riêng biệt
## Dependency inversion principle (DIP): Nguyên tắc đảo ngược phụ thuộc:
Các module cấp cao không nên phụ thuộc vào các module cấp thấp. Cả hai nên phụ thuộc vào các abstraction (trừu tượng). Các abstraction không nên phụ thuộc vào các chi tiết, mà các chi tiết nên phụ thuộc vào các abstraction.