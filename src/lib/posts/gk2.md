---
title: "Thiết kế hệ thống (Deliverable 2)"
date: "2025-05-30"
updated: "2025-05-30"
categories:
  - "sveltekit"
  - "markdown"

coverImage: "/images/thietkehethong.png"
coverWidth: 16
coverHeight: 9

---

## 1. Tổng quan kiến trúc hệ thống

![alt text](<../../../images/cấu trúc hệ thống.png>)


## 2. Thành phần chính

### 1. Frontend (React/ViteJS): Vai trò

- Hiển thị giao diện người dùng.  
- Gửi yêu cầu API tới backend để lấy dữ liệu.  
- Hiển thị danh sách task, thông tin chi tiết, và các chức năng quản trị.

**Hoạt động:**

- Sử dụng Axios để gửi yêu cầu HTTP tới backend.  
- Render dữ liệu nhận được từ backend bằng các component React.

---

### 2. Backend (Python Flask): Vai trò

- Xử lý yêu cầu từ frontend.  
- Thực hiện các thao tác CRUD (thêm, sửa, xóa, lấy dữ liệu) trên cơ sở dữ liệu pickledb.  
- Quản lý xác thực và phân quyền người dùng.

**Hoạt động:**

- Nhận yêu cầu HTTP từ frontend qua RESTful API.  
- Thao tác trực tiếp với pickledb để lưu trữ và truy xuất dữ liệu.  
- Trả về dữ liệu JSON cho frontend.


---

## 3. Mô hình dữ liệu chính (đơn giản)

- **User:**  
  - `id`  
  - `username`  
  - `email`  
  - `password`  

- **Task:**  
  - `id`  
  - `title`  
  - `description`  
  - `due_date`  
  - `status`  
  - `priority`  
  - `created_by`  
  - `assigned_user`

---

## 4. Chi tiết kế hoạch triển khai

### A. Backend với Flask + pickledb

- Tạo REST API cho các chức năng:  
  - Đăng ký, đăng nhập (với xác thực token đơn giản hoặc session)  
  - Thêm, sửa, xóa, lấy task  
  - Dashboard thống kê task theo trạng thái, user  
- Quản lý dữ liệu trong pickledb:  
  - Lưu `users` (dictionary theo username)  
  - Lưu `tasks` (dictionary theo id task)  
- Sử dụng Flask-CORS cho phép frontend gọi API từ domain khác  
- File dữ liệu pickledb lưu dưới dạng JSON, dễ backup và quản lý

### B. Frontend React + ViteJS

- Xây dựng giao diện đăng nhập, đăng ký, danh sách task, dashboard, form thêm/sửa task  
- Lưu token và username trong localStorage hoặc Context để xác thực  
- Gọi API backend qua Axios  
- Hiển thị thông báo lỗi, thành công bằng react-hot-toast hoặc tương tự

### C. Triển khai

- Backend: triển khai lên Render hoặc dịch vụ cloud hỗ trợ Python Flask  
- Frontend: triển khai lên Vercel hoặc Netlify  
- Cấu hình biến môi trường API_URL tương ứng

---

## 5. Ưu điểm & hạn chế của pickledb trong dự án

### Ưu điểm
- Dễ dùng, không cần cài đặt DB
- Lưu trữ file JSON đơn giản
- Truy xuất dữ liệu cực nhanh do dùng hashtable lưu dữ liệu trực tiếp vào RAM

### Hạn chế
- Không phù hợp lưu trữ phức tạp, dữ liệu quan hệ phức tạptạp
- Bảo mật kém (cần thì phải tự viết logic mã hóa/giải mã)
- Tốn RAM, với 1 khối lượng dữ liệu lớn sẽ tốn nhiều thời hơn các DB khác và tốn nhiều dữ liệu do lưu trực tiếp vào RAM


---

## 6. Mẫu kiến trúc API backend cơ bản

| Endpoint          | Phương thức | Mục đích                        |
|-------------------|-------------|--------------------------------|
| `/register`       | POST        | Tạo user mới                   |
| `/login`          | POST        | Đăng nhập, trả token hoặc xác thực |
| `/tasks/<username>`| GET         | Lấy danh sách task của user    |
| `/task`           | POST        | Tạo task mới                   |
| `/task/<id>`      | PUT         | Cập nhật task                  |
| `/task/<id>`      | DELETE      | Xóa task                      |
| `/dashboard/<username>` | GET    | Lấy thống kê task cho user    |



---

End