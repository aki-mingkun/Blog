---
title: "Deliverable 4"
date: "2025-05-31"
updated: "2025-05-31"
categories:
  - "sveltekit"
  - "markdown"

coverImage: "/images/pickleDB.png"
coverWidth: 16
coverHeight: 9

---



# Tiêu chí bắt buộc

---

## 1. Fault Tolerance (Chịu lỗi)
- **Đã đáp ứng một phần**

### Backend (Flask)
- Chạy trong container Docker, có cấu hình `restart: unless-stopped` giúp tự động khởi động lại nếu container dừng bất thường.
- Nếu backend gặp lỗi hoặc mất dữ liệu:
  - Toàn bộ chức năng backend sẽ bị ảnh hưởng.
  - Chỉ có một instance backend, không có dự phòng.
  - Chưa có cơ chế tự động chuyển đổi (failover), nhiều backend chạy song song hoặc cân bằng tải.

### Database (PickleDB)
- Là cơ sở dữ liệu file-based, không hỗ trợ replication, backup hay failover.
- Nếu file `tasks.db` bị hỏng hoặc mất, toàn bộ dữ liệu sẽ mất mà không thể phục hồi.

### Frontend (React)
- Chạy trong container Docker, có thể tự động khởi động lại nếu bị dừng.
- Tuy nhiên, không có dịch vụ cloud (như Vercel) để tự động giám sát và phục hồi ở mức nền tảng.

---

## 2. Distributed Communication (Giao tiếp phân tán)
- **Đã đáp ứng**

### Triển khai phân tán
- Các service (frontend, backend) có thể triển khai trên nhiều máy khác nhau bằng cách cấu hình địa chỉ IP/port.
- Docker hỗ trợ phân tán container trên nhiều host, giúp dễ dàng mở rộng.

### Giao tiếp qua HTTP REST API
- **Frontend ↔ Backend**: Frontend React sử dụng `axios` hoặc `fetch` để gọi API RESTful từ Flask backend.
- **Backend ↔ Database**: Flask backend thao tác trực tiếp với file PickleDB, không qua giao thức mạng.

### Đặc điểm phân tán thực sự
- Các thành phần có thể tách rời về máy chủ, nhưng hiện tại đang chạy gộp trên cùng một máy Docker host.
- Chưa có triển khai cloud hoặc multi-region, nhưng kiến trúc cho phép mở rộng.

---

## 3. Sharding hoặc Replication (Phân mảnh hoặc Sao chép dữ liệu)
**Chưa đáp ứng**

- Dữ liệu hiện chỉ lưu tập trung trên một backend duy nhất sử dụng PickleDB.
- Không có cơ chế phân mảnh (sharding) hoặc sao chép dữ liệu (replication).

### **Hướng phát triển**
- Có thể triển khai nhiều backend, mỗi backend lưu một phần dữ liệu (sharding theo user/task).
- Hoặc chuyển sang dùng hệ quản trị cơ sở dữ liệu mạnh hơn, hỗ trợ replication như MongoDB, PostgreSQL.

---

## 4. Simple Monitoring / Logging (Giám sát/ghi log đơn giản)
**Đã đáp ứng**

- Backend đã ghi log các request và lỗi ra console, có thể xem qua lệnh `docker logs`.
- Nếu cần, có thể mở rộng thêm:
  - Endpoint `/health` để kiểm tra trạng thái.
  - Dashboard log hoặc tích hợp công cụ giám sát (Prometheus, Grafana).

---
## 5. Basic Stress Test (Kiểm thử tải cơ bản)
 **Đã đáp ứng ở mức cơ bản**

- Có thể thực hiện kiểm thử tải bằng cách chia sẻ ip mạng của máy chủ cho các máy khác.
---

End