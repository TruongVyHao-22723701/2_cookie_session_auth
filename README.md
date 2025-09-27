# 2_cookie_session_auth
npm install express


Mở terminal run : node app.js

## -Register

**Register thành công:** 

Trong postman , chọn POST và nhập URL: http://localhost:3000/auth/register

Mở tab body -> raw json -> nhập thông tin đăng ký : 
{
  "username": "TruongVyHao",
  "password": "12345"
}
Send
-> Trả về : {
    "message": "User registered successfully!"
}
<img width="840" height="738" alt="image" src="https://github.com/user-attachments/assets/b9736055-2aa7-47d8-bd68-a33db8756bbc" />

User được lưu vào trong mongoDB trong collection users:
<img width="1254" height="849" alt="image" src="https://github.com/user-attachments/assets/b84c3fcf-52ef-4fc1-83b3-2a6578ac00d6" />

**Register thất bại:(trùng username hoặc password)** 

Sau khi đã đăng ký với username TruongVyHao, tiếp tục nhấn Send với URL cũ
-> Trả về: {
    "error": "User registration failed",
    "details": "E11000 duplicate key error collection: sessionAuth.users index: username_1 dup key: { username: \"TruongVyHao\" }"
}
<img width="842" height="747" alt="image" src="https://github.com/user-attachments/assets/81d39cf7-70dd-4243-b979-c93404f83127" />

**Register thất bại:(trống username,password)**

Trống password:
Tương tự, POST->URL: http://localhost:3000/auth/register -> body rawjson : 

{
  
  "username": "TruongVyHao",
  
  "password": ""
  
}

<img width="828" height="738" alt="image" src="https://github.com/user-attachments/assets/0074cb27-6477-48f1-89f8-bd64e0691f0a" />

Trống username:
{
  "username": "",
  "password": "12345"
}

<img width="832" height="745" alt="image" src="https://github.com/user-attachments/assets/f3e99b01-d914-4453-9ea4-9c752e973c3a" />


## -Login

**TH1: Login thành công**

Trong Postman, chọn POST và nhập URL: http://localhost:3000/auth/login, trong tab body -> raw json -> nhập thông tin đăng nhập(theo thông tin vừa register): {
  "username": "TruongVyHao",
  "password": "12345"
} 

Nhấn Send ->> Trả về: {
    "message": "Login successful!"
}
<img width="869" height="744" alt="image" src="https://github.com/user-attachments/assets/7ee4c9e5-48b6-49d6-9c2e-1c4c78d1d63b" />

Kiểm tra cookie:

Tab Cookies của Postman sẽ thấy cookie tên connect.sid được set.
<img width="918" height="605" alt="image" src="https://github.com/user-attachments/assets/96050901-e73a-49f8-8b8e-1b33da70aa55" />

Session được lưu trong MongoDB collection sessions.
<img width="1308" height="872" alt="image" src="https://github.com/user-attachments/assets/43ad91b7-51b9-405f-9421-2125221a0839" />


**TH2: Login thất bại ( Sai username,password )**

Trong Postman, chọn POST và nhập URL: http://localhost:3000/auth/login, trong tab body -> raw json -> nhập thông tin đăng nhập:
{
  "username": "TruongVyHao",
  "password": "adoijqowijdw"
}
->Send-> Trả về: "error": "Invalid username or password"
<img width="845" height="717" alt="image" src="https://github.com/user-attachments/assets/3523df54-be55-492e-a274-e5e409bbab34" />


## -Truy cập Profile

**TH1: Get/profile khi đã đập nhập**
Trong Postman, chọn GET và nhập URL: http://localhost:3000/auth/profile -> Send -> Kết quả trả về : {
    "_id": "68d539f196be8d6df284f246",
    "username": "TruongVyHao",
    "__v": 0
}
<img width="836" height="721" alt="image" src="https://github.com/user-attachments/assets/a69f2fc9-177e-4883-a98d-e6dff98acafe" />

**TH2: get/profile chưa login**
<img width="839" height="701" alt="image" src="https://github.com/user-attachments/assets/40ea3540-222d-43e7-994f-99b68c7c6917" />



## - Logout

Logout successful:
Trong Postman, chọn GET và nhập URL: http://localhost:3000/auth/logout -> Send -> Result: 
{
    "message": "Logout successful!"
}
<img width="851" height="761" alt="image" src="https://github.com/user-attachments/assets/f33771b2-18b3-477c-917d-a822f7a5549c" />

Cookie connect.sid bị xoá, session bị xoá khỏi MongoDB.
<img width="679" height="357" alt="image" src="https://github.com/user-attachments/assets/312f8a79-0ae1-40a2-b55d-50ec84fb2ef8" />
<img width="1175" height="919" alt="image" src="https://github.com/user-attachments/assets/a6fc984f-78da-4343-88d1-6fc92cd9d029" />
