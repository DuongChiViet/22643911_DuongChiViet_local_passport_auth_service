# Local Passport Authentication Service

Dự án xác thực người dùng sử dụng Passport.js với Local Strategy và MongoDB.

## 📑 Mục lục

- [⚙️ Cài đặt & Chạy dự án](#️-cài-đặt--chạy-dự-án)
- [🅰️ CÂU A](#️-câu-a)
  - [✨ Đăng ký tài khoản mới](#-đăng-ký-tài-khoản-mới)
  - [🗄️ Kiểm tra tài khoản đã lưu trong MongoDB](#️-kiểm-tra-tài-khoản-đã-lưu-trong-mongodb)
- [🅱️ CÂU B](#️-câu-b)
  - [🚫 Truy cập /auth/profile trước khi đăng nhập](#-truy-cập-authprofile-trước-khi-đăng-nhập)
  - [🔑 Đăng nhập vào hệ thống](#-đăng-nhập-vào-hệ-thống)
  - [👤 Truy cập /auth/profile sau khi đăng nhập](#-truy-cập-authprofile-sau-khi-đăng-nhập)

---

## ⚙️ Cài đặt & Chạy dự án

### 📦 Cài đặt dependencies

```bash
npm install
```

### ▶️ Chạy dự án

```bash
node app.js
```

Server sẽ chạy tại: `http://localhost:3000`

---

## 🅰️ CÂU A

### ✨ Đăng ký tài khoản mới

**Thực hiện POST request trong Postman:**

- **URL:** `http://localhost:3000/auth/register`
- **Method:** `POST`
- **Headers:** `Content-Type: application/json`
- **Body (JSON):**

```json
{
  "username": "admin",
  "password": "123456"
}
```

**Kết quả mong đợi:**
- Status: `201 Created`
- Response: Thông báo đăng ký thành công

📸 **Minh họa: Đăng ký tài khoản**
![Đăng ký tài khoản](screenshots/register.png)

### 🗄️ Kiểm tra tài khoản đã lưu trong MongoDB

Sau khi đăng ký thành công, bạn có thể kiểm tra tài khoản đã được lưu trong MongoDB:

1. Mở MongoDB Compass hoặc MongoDB Shell
2. Kết nối đến database của dự án
3. Kiểm tra collection `users`
4. Xác nhận tài khoản với username "admin" đã được tạo
5. Mật khẩu đã được hash bằng bcrypt

📸 **Minh họa: Tài khoản trong MongoDB**
![Tài khoản trong MongoDB](screenshots/mongodb-user.png)

---

## 🅱️ CÂU B

### 🚫 Truy cập /auth/profile trước khi đăng nhập

**Thực hiện GET request:**

- **URL:** `http://localhost:3000/auth/profile`
- **Method:** `GET`

**Kết quả mong đợi:**
- Status: `401 Unauthorized`
- Response: Thông báo yêu cầu đăng nhập

📸 **Minh họa: Chưa đăng nhập**
![Chưa đăng nhập](screenshots/profile-unauthorized.png)

### 🔑 Đăng nhập vào hệ thống

**Thực hiện POST request bằng Postman để đăng nhập:**

- **URL:** `http://localhost:3000/auth/login`
- **Method:** `POST`
- **Headers:** `Content-Type: application/json`
- **Body (JSON):**

```json
{
  "username": "admin",
  "password": "123456"
}
```

**Kết quả mong đợi:**
- Status: `200 OK`
- Response: Thông báo đăng nhập thành công
- Session được tạo và lưu trữ

📸 **Minh họa: Đăng nhập thành công**
![Đăng nhập thành công](screenshots/login-success.png)

### 👤 Truy cập /auth/profile sau khi đăng nhập

**Thực hiện GET request với session:**

- **URL:** `http://localhost:3000/auth/profile`
- **Method:** `GET`
- **Lưu ý:** Sử dụng cùng session/cookie từ request đăng nhập

**Kết quả mong đợi:**
- Status: `200 OK`
- Response: Thông tin profile của user đã đăng nhập

📸 **Minh họa: Truy cập profile sau đăng nhập**
![Truy cập profile sau đăng nhập](screenshots/profile-authorized.png)

---

## 🛠️ Cấu trúc dự án

```
📦 Local Passport Authentication Service
├── 📄 app.js                 # File chính của ứng dụng
├── 📄 package.json           # Dependencies và scripts
├── 📁 config/
│   └── 📄 passport.js        # Cấu hình Passport.js
├── 📁 models/
│   └── 📄 User.js            # Model User cho MongoDB
└── 📁 routes/
    └── 📄 auth.js            # Routes xử lý authentication
```

## 📚 Công nghệ sử dụng

- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **Passport.js** - Authentication middleware
- **MongoDB** - Database
- **Mongoose** - ODM cho MongoDB
- **bcrypt** - Hash mật khẩu
- **express-session** - Session management

## 🔧 API Endpoints

| Method | Endpoint | Mô tả | Auth Required |
|--------|----------|-------|---------------|
| POST | `/auth/register` | Đăng ký tài khoản mới | ❌ |
| POST | `/auth/login` | Đăng nhập | ❌ |
| GET | `/auth/profile` | Xem thông tin profile | ✅ |
| POST | `/auth/logout` | Đăng xuất | ✅ |

---

## 👨‍💻 Tác giả

**Dương Chí Việt** - MSSV: 22643911