---
title: "Deliverable 1: Đề xuất đề tài và mô tả vấn đề"
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
- Không thread-safe -> không phù hợp khi nhiều tiến trình cùng ghi vào DB.
- Không phù hợp cho dữ liệu lớn, vì lưu vào 1 file duy nhất, đọc/ghi sẽ chậm nếu dữ liệu nhiều.
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
- Lưu cấu hình ứng dụng: Cài đặt, tùy chọn người dùng.
- Bộ nhớ đệm: Lưu tạm kết quả tính toán, dữ liệu API.
- Quản lý phiên (đơn giản): Lưu thông tin đăng nhập (cho ứng dụng nhỏ).
- Lưu dữ liệu thử nghiệm: Mô phỏng database khi phát triển.
- Công cụ cá nhân: Quản lý việc, nhật ký, kết quả phân tích nhỏ.

---

## 2. Kế hoạch giữa kỳ

### Đề tài: Xây dựng 1 trang web quản lý công việc cá nhân với pickleDB

#### Bài toán đặt ra

- Trong dự án xây dựng trang web quản lý công việc cá nhân, bài toán cốt lõi mà pickleDB sẽ giải quyết là **lưu trữ và truy xuất thông tin** về các công việc (tiêu đề, mô tả, trạng thái, thời hạn, v.v.) **một cách cục bộ và đơn giản**.

#### Vấn đề

- **Làm sao để giao diện trực quan và dễ sử dụng?** Việc thiết kế một giao diện mà người dùng có thể dễ dàng thao tác, thêm, xem, chỉnh sửa và quản lý công việc một cách nhanh chóng và hiệu quả là rất quan trọng.

#### Giải pháp
*Tính đơn giản :*

- Giảm thiểu yếu tố không cần thiết: Chỉ hiển thị những thông tin và chức năng quan trọng nhất. Tránh làm người dùng bị choáng ngợp bởi quá nhiều tùy chọn.
- Bố cục rõ ràng: Sắp xếp các thành phần một cách logic và dễ hiểu. Sử dụng khoảng trắng hợp lý để tạo sự thông thoáng.
- Màu sắc hài hòa: Sử dụng bảng màu nhất quán và không quá sặc sỡ, tập trung vào việc truyền tải thông tin hiệu quả hơn là trang trí.

*Tính nhất quán :*

- Hiển thị rõ ràng các tùy chọn
- Sử dụng biểu tượng quen thuộc: Các biểu tượng (icons) nên mang ý nghĩa rõ ràng và phổ biến để người dùng dễ dàng nhận ra chức năng của chúng.

---

End