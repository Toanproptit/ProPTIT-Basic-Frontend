# Buổi 7: Hook ( gắn vào, móc vào)
## UseState 
+ **useState** giúp cập nhật lại trạng thái của dữ liệu (hay cập nhật lại giá trị của dữ liệu)
+ Khi dữ liệu thay đổi thì giao diện được cập nhật lại theo dữ liệu mới
+ Một vài ví dụ trong thực tế:
  + Bóng đèn có 2 trạng thái là bật hoặc tắt
  + Trạng thái đã đăng nhập hoặc chưa đăng nhập vào tài khoản
  + Khi tăng số lượng sản phẩm thì tổng tiền chưa được cập nhật lại.
## UsedEffect 
+ **useEffect** dùng để **xử lý logic** nào đó khi khi data được thay đổi
+ Component sau khi được render ra giao diện lần đầu , thì sẽ gọi tới hàm callback của useEffect ( vì chúng ta ưu tiên việc render ra giao diện trước, xử lí logic sau nên callBack của UseEffect sẽ chạy sau khi component được render ra).
+ Cú pháp:
    ```jsx
    useEffect(callback,[dependency]);
    ```
+ Trong đó:
  + **callback**: làm hàm gọi lại, bắt buộc phải có.
  + **dependency**: là một biến . Không bắt buộc phải có.

### TH1.useEffect(callback)
+ khi render lại giao diện (tức render lần 2 trở đi), thì callback của useEffect vẫn được gọi lại.
+ Ví dụ: querySelectorAll các item trong DOM

```jsx
import { useEffect } from "react";

function UseEffect1() {

    
    useEffect( () =>{
        let listItem = document.querySelectorAll("ul")
        console.log(listItem);
    })
    return(
        <>
        <ul>
            <li>Mục 1</li>
            <li>Mục 2</li>
            <li>Mục 3</li>
        </ul>
        </>
    )
}
export default UseEffect1;
```
### TH2.useEffect(callback,[])

+ Ví dụ: useEffect(callback,[])
+ Khi render lại giao diện(tức là lần 2 trở đi) thì **callback** của useEffect không được gọi lại.
+ Thường áp dụng cho gọi API 1 lần để lấy dữ liệu.

### TH3.useEffect(callback,[dependency])
+ Khi render Lại giao diện (tức render lần 2 trở đi), thì callback của useEffect được gọi lại khi dependency thay đổi
+ Ví dụ: Phân trang

## UseContext
+ UseContext (bối cảnh) giúp đơn giản hóa việc chuyển dữ liệu từ component cha xuống các component con mà không cần sử dụng đến props
+ Tức là chuyển trực tiếp từ component cha xuống các component con mà không cần phải thông qua 1 component gián tiếp.

Hình ảnh minh Họa:

![alt text](./AnhBuoi7/Anh1.png)

+ Các bước để sử dụng useContext:
  + Bước 1: Tạo ra một bối cảnh ở component A(để tạo ra phạm vi và sử dụng được data trong phạm vi đó, ví dụ phạm vi là component A thì tất cả các component con đều sử dụng được).
  
  ```jsx
  import {creatContext} from "react";
  exprort const AContext = creatContent();
  ```
  + Bước 2: Cung cấp bối cảnh  để bao bọc toàn bộ các component cần sử dụng data
  ```jsx
  function A(){
    return(
        <AContext.Provider value = {data}>
        <B />
        </Acontext.Provider >
    )
  }
  ```
  ![alt text](./AnhBuoi7/Anh2.png)

## UseRef
+ useRef trả về một object với thuộc tính current được khởi tạo thông qua tham số truyền vào.
+ Object được trả về không bị khởi tạo khi component render lại
+ Giá trị trong object thay đổi nhưng component không bị render lại (useState thay đổi thì làm component render lại)
+ Cú pháp:
```jsx 
const tenBien = useRef(initialValue);
```
+ Trong đó:
  + initialValue: là giá trị khởi tạo.
+ useRef được sử dụng để truy cập được các phần tử trong DOM
Ví dụ:
```jsx
import { useRef } from "react";

function UseRef1(){


    const counterRef = useRef(0)

    const handleClick = () => {
        counterRef.current +=1
    }
    
    console.log(counterRef.current)

    return(
        <>
        <button onClick={handleClick}>Click me</button>
        </>
    )
}
export default UseRef1;
```
Kết quả: ta thấy khi click mặc dù giá trị thay đổi nhưng component không được render lại

Ví dụ áp dụng:
+ Đếm được số lần component render lại.
+ Giới hạn lượt trúng thưởng
+ focus vào 1 input

## UseCallback
+ useCallback giúp tránh thực hiện lại một hàm không cần thiết
+ Giúp tạo ra một vùng nhớ để lưu hàm callBack và chỉ tạo ra hàm Callback mới khi dependencies thay đổi
+ Cú pháp: 
```jsx
const functionName = useCallback(callback,dependency)
```
Trong đó:
  + callback: là một hàm được gọi lại, lần render đầu tiên luôn chạy vào hàm này.
  + dependency: là sự phụ thuộc , khi dependency thay đổi thì useCallback mới tạo ra một hàm mới.
## UseMemo
+ useMemo giúp tránh thực hiện lại một logic không cần thiệt
+ useMemo tạo ra một vùng nhớ để lưu giá trị đầu ra và chỉ ghi nhớ giá trị mới khi dependencies thay đổi
+ Cú pháp: 
```jsx
const variableName  = useMemo(callback,dependency);
```
Trong đó:
  + callback: là một hàm được gọi lại, lần render đầu tiên luôn chạy vào hàm này.
  + dependency: là sự phụ thuộc , khi dependency thay đổi thì useMemo mới tạo ra một hàm mới.

Sự khác biệt giữa useCallback và useMemo:
  + useCallback lưu vào bộ nhớ một hàm.
  + useMemo lưu vào bộ nhớ một giá trị
  
Ví dụ:
```jsx
import { useMemo, useState } from "react";

function UseMemo1(){

    const [counter,setCounter] = useState(0)


    const handleClick = () =>{
        setCounter(counter+1);
    }

    const pow = () =>{
        console.log("chay ham pow");
        const res = Math.pow(10,3);
        return res;
    }
    // const result = pow();
    const result = useMemo( () =>{
        pow();
    },[])

    return(
        <>
        <div> kết quả: {counter}</div>
        <button onClick={handleClick}>Click me</button>
        <div>{result}</div>
        </>

    )
}
export default UseMemo1;
```
## UseReducer
+ useReducer giống như một phiên bản nâng cao của useState.
+ useReducer được sử dụng trong trường hợp component có state phức tạp
+ Cú pháp:
```jsx
const [state,dispatch] = useReducer(reducer,initialState);
```
+ Các bước sử dụng useReducer:
![alt text](./AnhBuoi7/Anh3.png)

## Quản lý Global State
* Cài đặt **React Signify** - công cụ quản lý Global State
```
npm i react-signify
```
**Khởi tạo Global State trong 3 bước**

Bước 1 : Khai báo global state
Cách khai báo rất đơn giản với 1 dòng code như sau:
```jsx
export const sCount = signify(0);
```

Bước 2 : Sử dụng giá trị
Cách sử dụng khá đơn giản bằng cách sử dụng hook use
```jsx
const count = sCount.use();
```
Bước 3 : Thay đổi giá trị
Đầu tiên ta tạo 1 function đại diện xử lý thay đổi +1 giá trị
```jsx
// Tạo function xử lý
const handleUp = () => {
  sCount.set((p) => (p.value += 1));
};
```
Tiếp theo, ứng dụng function này lên button của màn hình
```jsx
<button onClick={handleUp}>UP</button>
```

**Tổng quan code**

```jsx
// App.jsx
import { signify } from "react-signify";

export const sCount = signify(0); // 1. Khởi tạo Global State

export default function App() {
  const count = sCount.use(); // 2. Sử dụng Global State

  const handleUp = () => {
    sCount.set((p) => (p.value += 1)); // 3. Thay đổi giá trị Global State
  };
  
  return (
    <div>
      App {count}
      <button onClick={handleUp}>UP</button>
    </div>
  );
}
```

## React Router

### Giới thiệu

+ React Router là một thư viện được viết bằng React để quản lí routing trong các ứng dụng web.
+ Ví dụ:
  + Trang chủ : https://domain.com
  + Trang liên ệ: http://domain.com/contact
  + Trang blog: https://domain.com/blog
+ Link cài đặt trên trang NPM: https://www.npmjs.com/package/react-router-dom
+ Trang chủ: https://reactrouter.com/
+ Câu lệnh cài đăt: npm install react-router-dom

### Cách sử dụng components của React Router

+ **BrowserRouter**: để kết nối ứng dụng của bạn với URL của trình duyệt thì phải import BrowserRouter và bọc nó bên ngoài toàn bộ ứng dụng chính là component App
+ **Routes**: Cung cấp các tuyến đường(routes) để điều hướng các thành phần của ứng dụng React. Dùng để bọc bên ngoài danh sách các Route
+ **Route**: Được sử dụng để định nghĩa route để điều hướng đến một component cụ thể
+ **Link**: cho phép chuyển đổi giữa các URL khác nhau mà không cần phải load lại trang (nó tương tự như thẻ `<a>` trong HTML nhưng thẻ `<a>` sẽ load lại trang)
+ **Outlet**: Nó dùng để xác định vị trí mà component trong route được hiển thị (Sử dụng giống {props.children} trong React)
+ **NavLink**: cũng giống với link, nhưng nếu URL trùng với link của NavLink thì sẽ thêm class là active
+ **Navigate**: Sử dụng Navigate để tự động chuyển hướng đến một trang nào đó.

demo:
  
```jsx
import { Route, Routes } from "react-router-dom"
import Home from "./pages/Home"
import About from "./pages/About"
import Contact from "./pages/Contact"
import Eroll from "./pages/Errol"

function App() {

  return (
    <>
     <Routes>
      <Route path="/" element={<Home/>}/>
      <Route path="/about" element = {<About/>}/>
      <Route path="/contact" element = {<Contact/>}/>
      <Route path="*" element = {<Eroll/>}/>
     </Routes>
    </>
  )
}

export default App

```

```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'
import {BrowserRouter} from 'react-router-dom'

createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
)
```

Ví dụ về Link:
```jsx
import { Link } from "react-router-dom"

function Layout(){
    return(
        <>
        <div>
            <ul>
                <li>
                    <Link to="/">Home</Link>
                    <Link to="/about">About</Link>
                    <Link to="/contact">Contact</Link>

                </li>
            </ul>
        </div>
        </>
    )
}
export default Layout;
```
Kết quả là:
![alt text](./AnhBuoi7/Anh4.png)


```jsx
import { Route, Router, Routes } from "react-router-dom"
import Home from "./pages/Home"
import About from "./pages/About"
import Contact from "./pages/Contact"
import Eroll from "./pages/Errol"
import Layout from "./layout/Layout"

function App() {

  return (
    <>
    
     <Routes>
      <Route path="/" element={<Layout/>}>
        <Route path="/" element={<Home/>}/>
        <Route path="/about" element = {<About/>}/>
        <Route path="/contact" element = {<Contact/>}/>
        <Route path="*" element = {<Eroll/>}/>
      </Route>
     </Routes>
    </>
  )
}

export default App
``` 
Khi tôi bọc thằng layout bên ngoài thì chúng ta thấy được rằng những thành phần trong nó k hiện lên:

![alt text](./AnhBuoi7/Anh5.png)

Chính vì thế ta cần dùng đến **Outlet**:
```jsx
import { Link, Outlet } from "react-router-dom"

function Layout(){
    return(
        <>
        <div>
            <ul>
                <li>
                    <Link to="/">Home</Link>
                    <Link to="/about">About</Link>
                    <Link to="/contact">Contact</Link>
                </li>
                <div>
                    {/* Nội dung chính */}
                    <Outlet/>
                </div>
            </ul>
        </div>
        </>
    )
}
export default Layout;
```
kết quả là:
![alt text](./AnhBuoi7/Anh6.png)

## Index routes
+ Để hiển thị component ở route con ra ngoài route cha.
+ Như ví dụ ở trên khi truy cập vào http://domain.com/blog sẽ load component Blog và không hiển thị component con nào cả
+ Điều chúng ta mong muốn vẫn là URL như vậy những vẩn hiển thị một component con nào đó ở ngay component cha.
+ Để làm được điều này chúng ta cần sử dụng index và truyền component con muốn được hiển thị

chúng ta hiểu đơn giản là, khi mình thay index thay vì dùng path trong router thì khi chúng ta truy cập đến cha của nó, nó sẽ cùng được hiển thị với Router cha.

## Dynamic Router
+ Dynamic routes giúp chúng ta tạo ra được các router động

## Hook của React Router
+ **useParams**: Dùng để lấy được tham số trên param
+ **useNavigate**: Dùng để Điều hướng đến một đường dẫn khác, hoặc trở về các trang trước đó đã truy cập
![alt text](./AnhBuoi7/Anh7.png)

## Protected routes
+ Giả sử ứng dụng của chúng ta có 2 phần: public và private:
  + phần public thì ai cũng có thể truy cập được như trang chủ trang blog...
  + phần private thì phải đăng nhập vào mới xem được như trang thông tin cá nhân ,...
+ Về hành vi đối tượng với người dùng.
  + Nếu đăng nhập rồi thì truy cập được tất cả các link của public hay private
  + Nếu chưa thì chỉ truy cập được các trang public , nếu người dùng vẫn cố truy cập vào các trang private thì ta điều hướng họ sang trang login
  

# 📌 Route Object trong React Router

## 1. Route Object là gì?

* Trong **React Router v6.4+**, ngoài cách khai báo route bằng JSX (`<Routes><Route /></Routes>`), ta còn có thể khai báo route bằng **Route Object**.
* Route Object là **cấu hình dạng JavaScript object** mô tả các route của ứng dụng.

---

## 2. Cú pháp cơ bản

```jsx
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import Home from "./pages/Home";
import About from "./pages/About";
import NotFound from "./pages/NotFound";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Home />,
  },
  {
    path: "about",
    element: <About />,
  },
  {
    path: "*",
    element: <NotFound />,
  },
]);

export default function App() {
  return <RouterProvider router={router} />;
}
```

---

## 3. Các thuộc tính phổ biến trong Route Object

| Thuộc tính       | Ý nghĩa                                                                 |
| ---------------- | ----------------------------------------------------------------------- |
| **path**         | Chuỗi đường dẫn (ví dụ: `"about"`, `"contact/:id"`)                     |
| **element**      | React component được render khi path khớp                               |
| **children**     | Mảng các route con (dùng cho nested route)                              |
| **errorElement** | Component hiển thị khi có lỗi (error boundary cho route)                |
| **loader**       | Hàm async để load dữ liệu trước khi render route                        |
| **action**       | Hàm xử lý dữ liệu (thường cho form submission)                          |
| **id**           | Đặt định danh cho route (dùng trong `useRouteLoaderData`, `useFetcher`) |

---

## 4. Ví dụ Nested Routes

```jsx
import Layout from "./layout/Layout";
import Contact from "./pages/Contact";
import ContactDetail from "./pages/ContactDetail";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Layout />,
    children: [
      { path: "contact", element: <Contact /> },
      { path: "contact/:id", element: <ContactDetail /> },
    ],
  },
]);
```

---

## 5. So sánh với JSX Route

### Cách viết JSX:

```jsx
<Routes>
  <Route path="/" element={<Layout />}>
    <Route path="contact" element={<Contact />} />
    <Route path="contact/:id" element={<ContactDetail />} />
  </Route>
</Routes>
```

### Cách viết Route Object:

```jsx
const router = createBrowserRouter([
  {
    path: "/",
    element: <Layout />,
    children: [
      { path: "contact", element: <Contact /> },
      { path: "contact/:id", element: <ContactDetail /> },
    ],
  },
]);
```

👉 Cả hai cách đều tương đương, nhưng **Route Object mạnh hơn** vì hỗ trợ `loader`, `action`, `errorElement`.

---

## 6. Khi nào dùng Route Object?

* Khi bạn muốn **data loading** hoặc **form handling** gắn trực tiếp với route.
* Khi cần **error boundary** riêng cho từng route.
* Khi muốn cấu hình route tập trung thay vì rải rác trong JSX.

---

✍️ Tóm lại:
**Route Object** là cách mới, mạnh mẽ và linh hoạt hơn để khai báo routing trong React Router v6.4+.
Nó giúp tách biệt phần cấu hình routing và phần UI, đồng thời hỗ trợ nhiều tính năng nâng cao như loader, action, errorElement.

---


Ok 👍 mình sẽ viết tiếp phần **STATE MANAGEMENT** dưới dạng tài liệu/ghi chú Markdown để bạn dễ dùng trong bài học/presentation.

---

# 📌 PHẦN 3: STATE MANAGEMENT: ZUSTAND, REDUX TOOLKIT,...

## 1. Tại sao cần State Management?

* Khi ứng dụng React nhỏ, ta có thể dùng **useState** và **props** để truyền dữ liệu.
* Nhưng khi ứng dụng lớn, nhiều component cần chia sẻ state → props drilling trở nên rườm rà.
* Giải pháp: dùng **state management library** để:

  * Quản lý state tập trung
  * Dễ debug, dễ mở rộng
  * Giảm props drilling

---

## 2. Zustand (cơ bản)

### 🔹 Giới thiệu

* **Zustand** là thư viện state management nhẹ, đơn giản, hiệu năng cao.
* Khác với Redux, Zustand không cần nhiều boilerplate (reducer, action types...).
* Chỉ cần định nghĩa một store là có thể dùng ở bất kỳ component nào.

### 🔹 Cài đặt

```bash
npm install zustand
```

### 🔹 Ví dụ cơ bản

```jsx
import { create } from "zustand";

// Tạo store
const useCounterStore = create((set) => ({
  count: 0,
  increase: () => set((state) => ({ count: state.count + 1 })),
  decrease: () => set((state) => ({ count: state.count - 1 })),
}));

// Component
function Counter() {
  const { count, increase, decrease } = useCounterStore();
  
  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={increase}>+</button>
      <button onClick={decrease}>-</button>
    </div>
  );
}
```

👉 Ưu điểm: dễ dùng, ít code, không cần Provider.

---

## 3. Redux Toolkit (cơ bản)

### 🔹 Giới thiệu

* **Redux Toolkit (RTK)** là cách viết Redux mới, giảm boilerplate, dễ dùng hơn Redux cũ.
* Hỗ trợ:

  * **createSlice**: gộp reducer + action
  * **configureStore**: tạo store dễ dàng
  * Tích hợp tốt với middleware (thunk, saga)

### 🔹 Cài đặt

```bash
npm install @reduxjs/toolkit react-redux
```

### 🔹 Ví dụ cơ bản

```jsx
import { configureStore, createSlice } from "@reduxjs/toolkit";
import { Provider, useDispatch, useSelector } from "react-redux";

// 1. Tạo slice
const counterSlice = createSlice({
  name: "counter",
  initialState: { value: 0 },
  reducers: {
    increment: (state) => { state.value += 1 },
    decrement: (state) => { state.value -= 1 },
  },
});

export const { increment, decrement } = counterSlice.actions;

// 2. Tạo store
const store = configureStore({
  reducer: {
    counter: counterSlice.reducer,
  },
});

// 3. Component sử dụng
function Counter() {
  const value = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      <h2>Count: {value}</h2>
      <button onClick={() => dispatch(increment())}>+</button>
      <button onClick={() => dispatch(decrement())}>-</button>
    </div>
  );
}

// 4. App bọc Provider
export default function App() {
  return (
    <Provider store={store}>
      <Counter />
    </Provider>
  );
}
```

👉 Ưu điểm: chuẩn công nghiệp, mạnh mẽ, dễ scale khi app lớn.

---

## 4. So sánh nhanh

| Tiêu chí            | Zustand            | Redux Toolkit                              |
| ------------------- | ------------------ | ------------------------------------------ |
| Boilerplate         | Rất ít             | Ít hơn Redux cũ nhưng vẫn cần slice, store |
| Học dễ/nhanh        | ✅ Dễ               | ⚠️ Hơi khó hơn                             |
| Quy mô app          | App nhỏ-trung bình | App vừa-lớn                                |
| Debug/Tooling       | Không nhiều        | Redux DevTools cực mạnh                    |
| Tích hợp middleware | Thủ công           | Có sẵn (thunk, saga, middleware)           |

---

👉 **Kết luận:**

* **Zustand**: phù hợp khi cần quản lý state gọn, nhanh, ít cấu hình.
* **Redux Toolkit**: phù hợp khi app lớn, cần nhiều tính năng nâng cao và debug mạnh mẽ.

---

Bạn có muốn mình viết thêm một **ví dụ nâng cao** (ví dụ: fetch API với Zustand và Redux Toolkit) để thấy sự khác biệt rõ hơn không?


