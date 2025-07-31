# Buổi 5 ,JS phần 2
## Phần 1: JS ASYNC, API
### JS ASYNC
#### JSON:
+ JSON là định dạng để lưu trữ và vận chuyển dữ liệu.
+ JSON thường được sử dụng khi dữ liệu được gửi từ máy chủ đến trang web.
+ Cú pháp JSON được lấy từ cú pháp ký hiệu đối tượng JavaScript, nhưng định dạng JSON chỉ là văn bản. Mã để đọc và tạo dữ liệu JSON có thể được viết bằng bất kỳ ngôn ngữ lập trình nào.

Ví dụ về JSON:
```json
{
"employees":[
  {"firstName":"John", "lastName":"Doe"},
  {"firstName":"Anna", "lastName":"Smith"},
  {"firstName":"Peter", "lastName":"Jones"}
]
}
```

**Định dạng JSON đánh giá thành các đối tượng JavaScript**

+ Định dạng JSON về mặt cú pháp giống hệt với mã để tạo đối tượng JavaScript.

+ Nhờ vào sự tương đồng này, chương trình JavaScript có thể dễ dàng chuyển đổi dữ liệu JSON thành các đối tượng JavaScript gốc.

**Quy tắc cú pháp JSON**
+ Dữ liệu nằm trong cặp tên/giá trị
+ Dữ liệu được phân tách bằng dấu phẩy
+ Các thanh giằng xoắn giữ các vật thể
+ Dấu ngoặc vuông giữ mảng

**Dữ liệu JSON - Tên và Giá trị**

+ Dữ liệu JSON được viết dưới dạng cặp tên/giá trị, giống như thuộc tính đối tượng JavaScript.

+ Cặp tên/giá trị bao gồm tên trường (trong dấu ngoặc kép), theo sau là dấu hai chấm, rồi đến giá trị:
```json
"first Name":"Toan"
```
Tên JSON yêu cầu dấu ngoặc kép. Tên JavaScript thì không.

**Đối tượng JSON**
+ Các đối tượng JSON được viết bên trong dấu ngoặc nhọn.
+ Giống như trong javaScript, các đối tượng có thể có chứa nhiều cặp tên/giá trị:
```json
{"firstName":"Toan","lastName":"Nguyen"}
```
**Mảng JSON**
Mảng được viết trong dấu ngoặc vuông.
Giống như trong javaScript, một mảng có thể chứa các đối tượng:

```json
"employees":[
  {"firstName":"John", "lastName":"Doe"},
  {"firstName":"Anna", "lastName":"Smith"},
  {"firstName":"Peter", "lastName":"Jones"}
]
```
Trong ví dụ trên, đối tượng "employees" là một mảng, bao gồm ba đối tượng.

Mỗi đối tượng là một bản ghi về một người (có tên và họ).

**Chuyển đổi văn bản JSON thành JavaScript**

+ Một ứng dụng phổ biến của JSON là đọc dữ liệu từ máy chủ web và hiển thị dữ liệu trên trang web.

+ Để đơn giản, điều này có thể được chứng minh bằng cách sử dụng một chuỗi làm đầu vào.

+ Đầu tiên, hãy tạo một chuỗi JavaScript có chứa cú pháp JSON:

```js
let text = '{ "employees" : [' +
'{ "firstName":"John" , "lastName":"Doe" },' +
'{ "firstName":"Anna" , "lastName":"Smith" },' +
'{ "firstName":"Peter" , "lastName":"Jones" } ]}';
```
Sau đó sử dụng hàm tích hợp của js là JSON.parse() để chuyển đổi thành đối tượng js:
```js
const obj = JSON.parse(test);
```
Cuối cùng , hãy sử dụng đối tượng JS mới trong trang của bạn:
```html
<h1>Test JSON</h1>
    <p id="demo"></p>
    <script>
        let text = '{"employee":['+
        '{"firstName":"John", "lastName":"Doe"},'+
        '{"firstName":"Anna", "lastName":"Smith"},'+
        '{"firstName":"Peter", "lastName":"Jones"}]}';
        let obj = JSON.parse(text);
        document.getElementById("demo").innerHTML =
        obj.employee[0].firstName + " " +obj.employee[0].lastName ;
    </script>
```
#### JS Async: Callback Hell, Promise, Async, Await
**1.Callback Hell**
Các hàm JavaScript được thực thi theo trình tự chúng được gọi. Không phải theo trình tự chúng được định nghĩa.

Ví dụ này sẽ hiển thị "hello, World!":
```html
    <h1>Test JSON</h1>
    <p id="demo"></p>
    <script>
       function mydisplay(some){
        document.getElementById("demo").innerHTML = some;
        }
        function myfirst(){
            mydisplay("Hello, World!");
        }
        function mysecond(){
            mydisplay("Tam biệt");
        }
        mysecond();
        myfirst();
    </script>
```
**Kiểm soát trình tự**
+ Đôi khi bạn muốn kiểm soát tốt hơn thời điểm thực hiện một chức năng.

+ Giả sử bạn muốn thực hiện một phép tính và sau đó hiển thị kết quả.

+ Bạn có thể gọi hàm máy tính ( myCalculator), lưu kết quả, sau đó gọi hàm khác ( myDisplayer) để hiển thị kết quả:

Ví dụ:
```html
<p id="demo"></p>

<script>
function myDisplayer(some) {
  document.getElementById("demo").innerHTML = some;
}

function myCalculator(num1, num2) {
  let sum = num1 + num2;
  return sum;
}

let result = myCalculator(5, 5);
myDisplayer(result);
</script>
```
Hoặc, bạn có thể gọi hàm máy tính ( myCalculator) và để hàm máy tính gọi hàm hiển thị ( myDisplayer):
```html
<p id="demo"></p>

<script>
function myDisplayer(some) {
  document.getElementById("demo").innerHTML = some;
}

function myCalculator(num1, num2) {
  let sum = num1 + num2;
  myDisplayer(sum);
}
```
Trong ví dụ trên, myDisplayerđược gọi là hàm gọi lại .

Nó được truyền đi myCalculator()như một đối số .

**Khi nào nên sử dụng Callback?**

Những ví dụ trên không có gì thú vị cả.

Chúng được đơn giản hóa để dạy bạn cú pháp gọi lại.

Nơi mà các lệnh gọi lại thực sự tỏa sáng là trong các hàm không đồng bộ, trong đó một hàm phải chờ một hàm khác (giống như chờ tệp tải).

Các hàm không đồng bộ sẽ được đề cập ở chương tiếp theo.

**2.Promise**

Promise Object Properties

Đối tượng JavaScript Promise có thể là:

+ Chưa giải quyết
+ Đã hoàn thành
+ Vật bị loại bỏ
Đối tượng Promise hỗ trợ hai thuộc tính: state và result .

Trong khi đối tượng Promise đang "chờ xử lý" (đang hoạt động), kết quả vẫn chưa được xác định.

Khi một đối tượng Promise được "thực hiện", kết quả sẽ là một giá trị.

Khi một đối tượng Promise bị "từ chối", kết quả sẽ là một đối tượng lỗi.

|myPromise.state	|myPromise.result|
|-|-|
|"chưa giải quyết"|	không xác định|
|"đã hoàn thành"|	một giá trị kết quả|
|"vật bị loại bỏ"|	một đối tượng lỗi|

Cách sử dụng promise
```js
myPromise.then(
  function(value) { /* code if successful */ },
  function(error) { /* code if some error */ }
);
```

Promise.then() có hai đối số , một đối số gọi lại để thành công và một đối số khác để thất bại.
Cả hai đều là tùy chọn, do đó bạn chỉ có thể thêm lệnh gọi lại khi thành công hoặc thất bại.

Ví dụ:
```js
<p id="demo"></p>
    <script>
        function display(text) {
            document.getElementById("demo").innerHTML = text;
        }
        let myPromise = new Promise(function(myResolve,myReject){
            let x = 0;
            if(x==0){
                myResolve("OK")
            }
            else  {
                myReject("Error")
            }
        });
        myPromise.then(
            function(value) { display(value); },
            function(error) { display(error); }
        );
    </script>
```
**3.Asynchronous JavaScript**
Các ví dụ được sử dụng trong chương trước đã được đơn giản hóa rất nhiều.

Mục đích của các ví dụ này là để chứng minh cú pháp của hàm gọi lại

Trong thế giới thực, lệnh gọi lại thường được sử dụng với các hàm không đồng bộ.

Một ví dụ điển hình là JavaScript `setTimeout()`.

```js
<h1 id="demo"></h1>

<script>
setTimeout(myFunction, 3000);

function myFunction() {
  document.getElementById("demo").innerHTML = "I love You !!";
}
</script>
```
Trong ví dụ trên, myFunctionđược sử dụng như một lệnh gọi lại.

myFunctionđược truyền đi setTimeout()như một đối số.

3000 là số mili giây trước khi hết thời gian chờ, do đó myFunction()sẽ được gọi sau 3 giây.

Thay vì truyền tên hàm làm đối số cho một hàm khác, bạn luôn có thể truyền toàn bộ hàm:
```js
 <p id="demo"></p>
    <script>
        setTimeout(function(){display("I love you")},4000);
        function display(text) {
            document.getElementById("demo").innerHTML = text;
        }
    </script>
```
Trong ví dụ trên, function(){ myFunction("I love You"); } được sử dụng như một hàm gọi lại. Đây là một hàm hoàn chỉnh. Hàm hoàn chỉnh được truyền cho setTimeout() dưới dạng đối số.

3000 là số mili giây trước khi hết thời gian chờ, do đó myFunction()sẽ được gọi sau 3 giây.
**Waiting for Intervals:**
Khi sử dụng hàm JavaScript `setInterval()`, bạn có thể chỉ định một hàm gọi lại để thực thi cho mỗi khoảng thời gian:
```js
<h1 id="demo"></h1>

<script>
setInterval(myFunction, 1000);

function myFunction() {
  let d = new Date();
  document.getElementById("demo").innerHTML=
  d.getHours() + ":" +
  d.getMinutes() + ":" +
  d.getSeconds();
}
</scrip
```
Trong ví dụ trên, myFunctionđược sử dụng như một lệnh gọi lại.

myFunctionđược truyền đi setInterval()như một đối số.

1000 là số mili giây giữa các khoảng thời gian, do đó myFunction()sẽ được gọi là mỗi giây.

**Các lựa chọn thay thế gọi lại**
+ Với lập trình không đồng bộ, các chương trình JavaScript có thể bắt đầu các tác vụ chạy lâu và tiếp tục chạy các tác vụ khác song song.

+ Tuy nhiên, chương trình bất đồng bộ rất khó viết và khó gỡ lỗi.

+ Vì lý do này, hầu hết các phương thức JavaScript bất đồng bộ hiện đại không sử dụng callback. Thay vào đó, trong JavaScript, lập trình bất đồng bộ được giải quyết bằng Promise .
  
**4,Async, Await**
+ async làm cho một hàm trả về một Promise

+ await làm cho một hàm chờ một Promise

Async - bất đồng bộ:

Từ khóa `async` trước một hàm khiến hàm đó trả về một lời hứa:

Ví dụ:
```js
async function myFunction() {
  return "Hello";
}
```
Giống như:
```js
function myFunction() {
  return "Hello";
}
```
Await-Chờ
Từ awaitkhóa chỉ có thể được sử dụng bên trong một asynchàm.

Từ khóa này await khiến hàm tạm dừng thực thi và chờ lời hứa được giải quyết trước khi tiếp tục:
```js
let value = await promise;
```
Ví dụ:
```js
async function myDisplay() {
  let myPromise = new Promise(function(resolve, reject) {
    resolve("I love You !!");
  });
  document.getElementById("demo").innerHTML = await myPromise;
}

myDisplay();
</script>
```

Hai đối số (giải quyết và từ chối) được JavaScript xác định trước.

Chúng ta sẽ không tạo chúng mà sẽ gọi một trong số chúng khi hàm thực thi đã sẵn sàng.

Thông thường chúng ta không cần hàm từ chối.

```js
<h2 id="demo"></h2>

<p>Wait 3 seconds (3000 milliseconds) for this page to change.</p>

<script>
async function myDisplay() {
  let myPromise = new Promise(function(resolve) {
    setTimeout(function() {resolve("I love You !!");}, 3000);
  });
  document.getElementById("demo").innerHTML = await myPromise;
}
```
Ví dụ Đang chờ thời gian chờ.

### FETCH API
**1,API**

API (Application Programming Interface) là cổng giao tiếp giữa các ứng dụng — ví dụ: giữa frontend và backend.

Ví dụ:
```http
GET https://example.com/api/users/42?status=active
```
+ Đây là một API lấy thông tin người dùng có `id = 42` và trạng thái `active`.

**2,Params**
Parmas là phần nằm trong đường dẫn (URL), thường có dạng `:id`,`usedId`...

Ví dụ cụ thể:
```http
GET /api/users/42
```
ở đây: 42 là Params, cụ thể là id=42
Trong code (giả sử bạn dùng Node.js/Express ở backend):
```js
app.get('/api/users/:id', (req, res) => {
  const userId = req.params.id; // lấy "42"
});
```
**3,Query**
Query là phần sau dấu ? trong URL, thường được dùng để lọc dữ liệu hoặc truyền thêm tùy chọn.

Ví dụ:
```http
GET /api/users/42?status=active&sort=name
```
status=active và sort=name là query parameters

**4,Body**
Body là dữ liệu gửi kèm trong request, chỉ dùng với POST,PUT,PATCH
Ví dụ cụ thể:
```http
POST /api/users
Content-Type: application/json

{
  "name": "Toàn",
  "age": 20
}

name và age là dữ liệu nằm trong body
```
**5,Fetch**
Fetch là hàm tích hợp trong JavaScript để gọi API

Ví dụ cụ thể:
Dùng fetch để gọi API
Mục tiêu của ví dụ: gửi POST tạo người dùng mới

```js
fetch('https://example.com/api/users'.{
    method:'Post',
    headers:{
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ name: 'Toan', age: 20 })
  })
  .then(response => response.json())
  .then(data => {
    console.log('Success:', data);
  })
  .catch((error) => {
    console.error('Error:', error);
  });
```
### REST API
1. Khái niệm
REST (REpresentational State Transfer) là một kiến trúc xây dựng API cho phép frontend (JS) gọi tới server để tạo, đọc, cập nhật, xóa dữ liệu — gọi tắt là CRUD.

2. Các hành động chính trong Rest API (CRud)

|Tên gọi|	HTTP Method	|Ý nghĩa|	Ví dụURL|
|-------|--------------|-------|----------|
|Create|	POST|	Tạo mới dữ liệu|	/api/users|
|Read	|GET|	Lấy dữ liệu	|/api/users hoặc |/api/users/42|
|Update|	PUT hoặc PATCH|	Cập nhật dữ liệu|	/api/users/42|
|Delete|	DELETE|	Xóa dữ liệu|	/api/users/42|

3. Cách Js (trình duyệt) gọi Rest API bằng Fetch

Ví dụ:

**A,Tạo dữ liệu mới - POST**
```js
fetch('https://example.com/api/users'.{
    method:'Post',
    headers:{
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ name: 'Toan', age: 20 })
  })
  .then(response => response.json())
  .then(data => {
    console.log('Success:', data);
  })
  .catch((error) => {
    console.error('Error:', error);
  });
```
gửi dữ liệu mới trong body
sever nhận vào tạo user mới

**B,Lấy danh sách dữ liệu - GET**
```js
fetch('https://example.com/api/users')
  .then(res => res.json())
  .then(users => console.log('Danh sách user:', users));
```
Dùng để đọc dữ liệu không có body.

**C, lấy dữ liệu cụ thể - GET/users/:id**

```js
fetch('https://example.com/api/users/42')
  .then(res => res.json())
  .then(users => console.log('Danh sách user:', users));
```
Lấy 1 user có ID là 42
42 ở đây là params(được gắn vào URL)

**D, Cập nhật dữ liệu PUT or PATCH**
```js
fetch('https://example.com/api/users/42', {
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'Toàn Updated',
    age: 21
  })
})
  .then(res => res.json())
  .then(data => console.log('Đã cập nhật:', data));
```
cập nhật user có id là 42

**E, Xóa dữ liệu-DELETE**
```js
fetch('https://example.com/api/users/42', {
  method: 'DELETE'
})
  .then(res => res.json())
  .then(data => console.log('Đã xoá:', data));
```
gửi lệnh xóa user có id là 42

### POST MAN
Postman là một phần mềm giúp chúng ta:
+ Gửi yêu cầu HTTP (GET,POST,PUT,DELETE) tới API sever
+ Gửi dữ liệu dạng params,query,body
+ Kiểm tra phản hổi(response)
+ Dùng thử API trước khi viết code

=> Nó giúp bạn kiểm tra API trước khi bạn viết hoặc trong khi viết JavaScrpt.

## Phần 2: STORAGE
### Storing Data
1,Cookie:
+ là dữ liệu nhỏ được lưu trên trình duyệt , nhưng tự động gửi kèm mỗi lần trình duyệt gọi đến server.
+ Dùng cho xác thực , lưu đăng nhập, tracking

Có thể được gửi kém theo HTTP request
Ví dụ:
```js
document.cookie = "username=Toan; expires=Fri, 31 Dec 2025 23:59:59 UTC; path=/";
```
Gửi cookie tới server (tự động khi gọi API nếu withCredentials = true)
Ưu điểm:
+ Có thể truy cập từ cả JS (client) lẫn server
+ Gửi tự động trong request → thích hợp cho xác thực truyền thống

Nhược điểm:
+ Dung lượng rất nhỏ (~4KB)

+ Dễ bị tấn công XSS nếu không bảo vệ kỹ

+ Phải xử lý phức tạp hơn

2,Local Storage
+ Lưu trữ dữ liệu vĩnh viễn trên trình duyệt (trừ khi người dùng xoá thủ công hoặc gọi clear).

Ví dụ:
```js
localStorage.setItem("theme", "dark");
console.log(localStorage.getItem("theme")); // "dark"
localStorage.removeItem("theme");
```

**Đặc điểm:**
+ Không tự gửi lên server

+ Dung lượng lớn hơn cookie (~5MB)

+ Dữ liệu vẫn tồn tại kể cả khi tắt máy, mở lại

**Ưu điểm:**
+ Đơn giản, nhanh

+ Dùng tốt để lưu cấu hình người dùng (theme, ngôn ngữ,...)

**Nhược điểm:**
+ Không bảo mật: Dễ bị truy cập bởi JS

+ Không thích hợp để lưu token bảo mật
3,Session Storage
Giống localStorage, nhưng chỉ tồn tại trong một session/tab.
Ví dụ:
```js
sessionStorage.setItem("temp", "123");
sessionStorage.getItem("temp"); // "123"
```
**Đặc điểm:**
Mất dữ liệu khi đóng tab/trình duyệt

Không tự gửi lên server

**Dùng khi:**
Cần lưu dữ liệu tạm thời, như dữ liệu đang nhập trong form chưa gửi, hoặc trạng thái khi mở 1 tab mới

### Token (Access Token, Refresh Token)
Token là một chuỗi ký tự đại diện cho quyền truy cập của người dùng.
|	Loại token|	Tác dụng|		Hạn dùng|	
|-|-|-|
|	Access Token|		Gửi lên API để chứng minh bạn đã đăng nhập	|	Ngắn hạn (vài phút - vài giờ)
|	Refresh Token|		Dùng để xin Access Token mới|		Dài hạn (vài ngày - vài tuần)

Lưu Token ở đâu?:
| Lựa chọn              | Ưu điểm                           | Nhược điểm               | Dùng khi                          |
| --------------------- | --------------------------------- | ------------------------ | --------------------------------- |
| **Cookie (HttpOnly)** | Bảo mật tốt, chống XSS            | Phải cấu hình thêm       | **Bảo mật cao, web truyền thống** |
| **localStorage**      | Dễ dùng                           | Dễ bị XSS tấn công       | SPAs, demo, app nhỏ               |
| **sessionStorage**    | Hạn chế XSS + tự hết khi đóng tab | Mất dữ liệu khi đóng tab | Tạm thời, bảo mật nhẹ             |

Ví dụ:
```js
localStorage.setItem('access_token', 'abc123');
fetch('/api/profile', {
  headers: {
    'Authorization': 'Bearer ' + localStorage.getItem('access_token')
  }
});
```