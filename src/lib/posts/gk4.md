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

### Hiện trạng
- Chỉ có **1 backend**, **1 file database**.
- Không có dự phòng, không có backup, không có failover.

### Giải pháp đề xuất
- **Backend:**
  - Chạy nhiều instance backend (scale out), đặt sau load balancer (Nginx, HAProxy).
  - Dùng Docker Swarm hoặc Kubernetes để tự động restart, thay thế container khi gặp sự cố.
- **Database:**
  - Chuyển sang database hỗ trợ replication, backup (PostgreSQL, MongoDB).
  - Thiết lập backup định kỳ (cron job copy file hoặc dump dữ liệu).
  - Nếu vẫn dùng PickleDB: viết script backup file `tasks.db` định kỳ sang nơi khác.
- **Frontend:**
  - Deploy trên cloud (Vercel, Netlify, AWS ECS) để tận dụng tự động phục hồi.
  - Sử dụng healthcheck endpoint để kiểm tra tình trạng backend.

---

## 2. Distributed Communication (Giao tiếp phân tán)
- **Đã đáp ứng một phần**

### Hiện trạng
- Các service giao tiếp qua HTTP REST API, có thể triển khai trên nhiều máy.

### Giải pháp đề xuất
- Đảm bảo địa chỉ API trong frontend **không hardcode localhost**.
- Sử dụng service discovery (Consul, etcd) nếu triển khai nhiều backend.
- Thêm HTTPS, xác thực API để đảm bảo bảo mật giao tiếp.

---

## 3. Sharding hoặc Replication (Phân mảnh hoặc Sao chép dữ liệu)
**Chưa đáp ứng**

### Hiện trạng
- Không có sharding hoặc replication, dữ liệu tập trung.

### Giải pháp đề xuất
- **Sharding:**
  - Nếu số lượng user lớn, chia nhỏ dữ liệu theo user (mỗi backend phụ trách một nhóm user).
  - Cần database hỗ trợ sharding (MongoDB, Cassandra).
- **Replication:**
  - Dùng database hỗ trợ replication (PostgreSQL, MongoDB) để có nhiều bản sao dữ liệu, tăng khả năng chịu lỗi.
  - Thiết lập master-slave hoặc multi-primary replication.
- **PickleDB không hỗ trợ các tính năng này, cần nâng cấp hệ quản trị cơ sở dữ liệu.**


---

## 4. Simple Monitoring / Logging (Giám sát/ghi log đơn giản)
**Đã đáp ứng một phần**

### Hiện trạng
- Log ra console, xem bằng `docker logs`.

### Giải pháp đề xuất
- Thêm endpoint `/health` ở backend để kiểm tra tình trạng service.
- Gửi log ra file hoặc tích hợp hệ thống log tập trung (ELK stack, Loki).
- Tích hợp Prometheus/Grafana để giám sát số lượng request, lỗi, thời gian phản hồi.
- Thiết lập alert khi backend không phản hồi hoặc log có lỗi nghiêm trọng.

---
## 5. Basic Stress Test (Kiểm thử tải cơ bản)
 **Đã đáp ứng ở mức cơ bản**

### Hiện trạng
- Kiểm thử tải thủ công bằng cách truy cập từ nhiều máy qua ip của máy cá nhân.

### Giải pháp
- Sử dụng công cụ stress test:
  - Apache JMeter
  - k6
  - Locust
- Mô phỏng nhiều user đồng thời, đo:
  - Thời gian phản hồi.
  - Tỷ lệ lỗi.
  - Ngưỡng chịu tải tối đa.
- Deploy web lên server riêng

---

End