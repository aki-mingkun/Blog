---
title: "Kế hoạch giữa kỳ"
date: "2025-05-10"
updated: "2025-05-10"
categories:
  - "sveltekit"
  - "markdown"

coverImage: "/images/pickleDB.png"
coverWidth: 16
coverHeight: 9

excerpt: Phân tích thư viện pickleDB và kế hoạch sử dụng thư viện này trong bài tập giữa kỳ môn Ứng dụng phân tán.
---



# Phân tích thư viện pickleDB và Kế hoạch bài giữa kỳ

## 1. Mục đích của thư viện pickleDB

### Mục đích và vấn đề giải quyết
- `pickleDB` là một thư viện key-value store nhẹ cho Python, sử dụng JSON làm backend lưu trữ.
- Lý tưởng cho các ứng dụng nhỏ, script đơn giản, không cần đến hệ quản trị cơ sở dữ liệu phức tạp.

> Khi cần lưu cấu hình, trạng thái, dữ liệu người dùng một cách nhanh gọn, `pickleDB` là lựa chọn tuyệt vời.

### Ưu điểm
- Nhẹ, không cần server.
- Cú pháp giống dictionary Python.
- Dữ liệu lưu dưới dạng JSON – dễ đọc và chỉnh sửa.
- Hỗ trợ thao tác cơ bản: set/get/delete và auto-save.

### Nhược điểm
- Không phù hợp cho dữ liệu lớn.
- Thiếu tính năng nâng cao như truy vấn phức tạp, bảo mật, truy cập đồng thời.

### So sánh với các thư viện/framework khác

| Thư viện | Ưu điểm | Nhược điểm |
|---------|---------|------------|
| **pickleDB** | Nhẹ, dễ dùng, không cần server | Giới hạn tính năng, không phù hợp cho hệ thống lớn |
| **TinyDB** | JSON-based, hỗ trợ query mạnh | Chậm nếu dữ liệu lớn |
| **Redis** | Hiệu năng cao, nhiều kiểu dữ liệu | Cần cài đặt server |
| **SQLite** | Có SQL, nhẹ, dùng phổ biến | Không phải NoSQL |
| **MongoDB** | Đa năng, mạnh mẽ | Yêu cầu cài đặt, phức tạp |

### Ứng dụng thực tế
- Quản lý cấu hình người dùng.
- Tạo cache tạm thời.
- Lưu trạng thái app CLI hoặc desktop.
- Học tập, giảng dạy NoSQL.

---

## 2. Kế hoạch giữa kỳ

### Đề tài: Xây dựng ứng dụng quản lý công việc cá nhân với pickleDB

#### Vấn đề
- Người dùng cần quản lý task một cách đơn giản, offline, không cần kết nối mạng hay hệ quản trị CSDL nặng.

#### Giải pháp
- Sử dụng `pickleDB` để lưu trữ thông tin task.
- Task gồm các thuộc tính: ID, nội dung, thời gian tạo, trạng thái.
- Cho phép thêm, sửa, xóa, hoàn thành task.
- Giao diện có thể là CLI hoặc GUI (Tkinter).
- Tính năng nâng cao (tuỳ chọn): độ ưu tiên, sắp xếp, thống kê.
