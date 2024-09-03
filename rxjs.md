### 1. Phân biệt Subject, BehaviorSubject, ReplaySubject, AsyncSubject:

| Subject | BehaviorSubject | ReplaySubject | AsyncSubject |
|------|-------|------|------|
| chỉ nhận data sau khi đã subscribe.|subscriber sẽ nhận được giá trị cuối cùng mà Subject emit.|Cũng tương tự BehaviorSubject, tuy nhiên dữ liệu đã emit được lưu lại với số lượng tùy ý (được cấu hình lúc khai báo). Khi subscriber bắt đầu subscribe thì nó sẽ nhận được số lượng giá trị đã emit trước đó tương ứng.|Chỉ emit giá trị cuối cùng lúc khi complete().|


### 2. Phân biệt mergeMap, switchMap, concatMap, exhaustMap

#### `MergeMap`
- Hoạt động: Khi nhận được giá trị từ Observable nguồn, mergeMap sẽ `tạo ra một Observable mới và hợp nhất tất cả các Observable đó vào cùng một luồng, bất kể thứ tự hoặc thời gian hoàn thành`.
- Ưu điểm: Xử lý các luồng song song, hiệu quả khi không cần quan tâm đến thứ tự hoặc hoàn thành trước sau của các Observable.
- Nhược điểm: Có thể gây ra tình trạng cạnh tranh (race conditions) khi các Observable hoàn thành không theo thứ tự mong muốn.
```typescript
source$.pipe(
    mergeMap(value => anotherObservable(value))
)
```
#### `switchMap`
- Hoạt động: Khi nhận được một giá trị mới từ Observable nguồn, switchMap sẽ `hủy bỏ bất kỳ Observable nào trước đó chưa hoàn thành và chỉ giữ lại Observable mới nhất`.
- Ưu điểm: Phù hợp khi chỉ cần quan tâm đến kết quả mới nhất, chẳng hạn khi xử lý tìm kiếm tự động hoặc yêu cầu mạng liên tục thay đổi.
- Nhược điểm: Các Observable trước đó có thể bị hủy bỏ, ngay cả khi chúng gần hoàn thành.
Ví dụ:
```typescript
source$.pipe(
    switchMap(value => anotherObservable(value))
)
```
#### `concatMap`
- Hoạt động: Khi nhận được giá trị từ Observable nguồn, concatMap sẽ đợi Observable trước đó hoàn thành trước khi bắt đầu xử lý Observable mới. Nó đảm bảo rằng các Observable được xử lý tuần tự theo thứ tự chúng được nhận.
- Ưu điểm: Duy trì thứ tự xử lý của các Observable, không để xảy ra tình trạng các yêu cầu bị chồng chéo.
- Nhược điểm: Không thể xử lý song song các Observable, có thể dẫn đến hiệu suất thấp hơn nếu có nhiều Observable.
```typescript
source$.pipe(
    concatMap(value => anotherObservable(value))
)
```
#### `exhaustMap`
- Hoạt động: Khi nhận được giá trị từ Observable nguồn, exhaustMap sẽ bỏ qua tất cả các giá trị tiếp theo cho đến khi Observable hiện tại hoàn thành. Khi hoàn thành, nó sẽ chấp nhận giá trị mới tiếp theo từ Observable nguồn.
- Ưu điểm: Tốt cho các tình huống yêu cầu chỉ cần xử lý một Observable tại một thời điểm và bỏ qua các yêu cầu liên tiếp nếu có một Observable đang chạy.
- Nhược điểm: Bỏ qua các giá trị nguồn khi Observable hiện tại chưa hoàn thành, có thể dẫn đến mất dữ liệu nếu có quá nhiều yêu cầu liên tiếp.
```typescript
source$.pipe(
    exhaustMap(value => anotherObservable(value))
)
```

### 3. Phân biệt map, mapTo

#### `map`
- Hoạt động: map biến đổi `mỗi giá trị` được phát ra từ Observable nguồn, dựa trên một `hàm biến đổi được cung cấp`. Nó cho phép bạn thực hiện bất kỳ phép biến đổi nào trên giá trị, từ thay đổi kiểu dữ liệu, thực hiện phép toán, đến kết hợp với các giá trị khác.
```typescript
of(1, 2, 3).pipe(
    map(value => value * 2)
).subscribe(console.log);
// 2
// 4
// 6
```
#### `mapTo`
- Hoạt động: mapTo biến đổi `tất cả các giá trị` phát ra từ Observable nguồn thành một `giá trị cố định`, bất kể giá trị ban đầu là gì. Nó được sử dụng khi bạn chỉ cần thay thế tất cả các giá trị phát ra bằng một giá trị duy nhất.
```typescript
of(1, 2, 3).pipe(
    mapTo(10)
).subscribe(console.log);
// 10
```

### 4. Phân biệt take, takeUntil, takeWhile, và skipWhile

#### `take`
- Hoạt động: take `phát ra` một `số lượng giá trị nhất định` từ Observable nguồn và sau đó hoàn thành.
```typescript
of(1, 2, 3, 4, 5).pipe(
    take(2)
).subscribe(console.log);
// 1
// 2
```
#### `takeUntil`
- Hoạt động: takeUntil `phát ra` các giá trị từ Observable nguồn `cho đến khi một Observable khác (gọi là notifier) phát ra một giá trị`, sau đó Observable nguồn sẽ hoàn thành ngay lập tức.
```typescript
const source$ = interval(1000);
const click$ = fromEvent(document, 'click');
source$.pipe(
    takeUntil(click$)
).subscribe(console.log);
// 0
// 1
// 2
// Tiếp tục cho đến khi nút bấm
```
#### `takeWhile`
-  Hoạt động: takeWhile `phát ra` các giá trị từ Observable nguồn `cho đến khi điều kiện nào đó không còn đúng`. Khi điều kiện trả về false, nó ngừng phát ra giá trị và hoàn thành Observable.
```typescript
of(1, 2, 3, 4, 5).pipe(
    takeWhile(value => value < 4)
).subscribe(console.log);
// 1
// 2
// 3
```
#### `skipWhile`
Hoạt động: skipWhile `bỏ qua` các giá trị phát ra từ Observable nguồn `cho đến khi điều kiện nào đó không còn đúng`. Sau đó, nó phát ra tất cả các giá trị còn lại, kể cả những giá trị vi phạm điều kiện.
```typescript
of(1, 2, 3, 4, 5).pipe(
  skipWhile(value => value < 3)
).subscribe(console.log);
// 3
// 4
// 5
```

### 5. Phân biệt combineLatest, zip, và forkJoin 

#### `combineLatest`
- Hoạt động: combineLatest `phát ra` `giá trị mới bất cứ khi có ít nhất một giá trị mới từ bất kỳ Observable nào trong danh sách`. Khi bất kỳ Observable nào phát ra một giá trị mới, combineLatest `kết hợp các giá trị hiện tại` từ tất cả các Observable và `phát ra một mảng các giá trị kết hợp`.
- Yêu cầu: Tất cả các Observable phải phát ra `ít nhất một giá trị trước khi combineLatest phát ra giá trị đầu tiên`.
```typescript
const obs1$ = of(1, 2, 3);
const obs2$ = of('A', 'B');
const obs3$ = of(true, false);
combineLatest([obs1$, obs2$, obs3$]).subscribe(console.log);
// [3, 'B', false]
```
#### `zip`
- Hoạt động: zip `kết hợp` các giá trị từ nhiều Observable theo nhóm. Nó phát ra `một mảng` các giá trị kết hợp khi tất cả các Observable phát ra một giá trị mới cùng lúc. Khi `bất kỳ` một Observable `không có giá trị mới để phát ra`, zip sẽ `hoàn thành` và không `phát ra giá trị mới nữa`.
- Yêu cầu: Tất cả các Observable phải phát ra `một giá trị cùng một lúc để zip phát ra một giá trị kết hợp`. Khi một  `Observable hoàn thành`, zip cũng sẽ `hoàn thành`.

```typescript
const obs1$ = of(1, 2, 3);
const obs2$ = of('A', 'B', 'C');
const obs3$ = of(true, false, true);
zip([obs1$, obs2$, obs3$]).subscribe(console.log);
// [1, 'A', true]
// [2, 'B', false]
// [3, 'C', true]
```
#### `forkJoin`
- Hoạt động: forkJoin `phát ra` một mảng các giá trị kết hợp khi `tất cả các Observable trong danh sách đã hoàn thành`. Nó chỉ phát ra giá trị khi tất cả các Observable đều hoàn thành. Nếu có bất kỳ Observable nào không hoàn thành, forkJoin sẽ không phát ra giá trị.
- Yêu cầu: `Tất cả các Observable phải hoàn thành` trước khi forkJoin phát ra giá trị. `Nếu bất kỳ Observable nào không hoàn thành`, forkJoin sẽ không phát ra giá trị.
```typescript
const obs1$ = of(1, 2, 3).toPromise();
const obs2$ = of('A', 'B').toPromise();
const obs3$ = of(true, false).toPromise();
forkJoin([obs1$, obs2$, obs3$]).subscribe(console.log);
// [[3], ['B'], false]
Output:
```
