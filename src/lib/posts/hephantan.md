---
title: "Hệ thống phân tán"
date: "2025-04-29"
updated: "2025-04-29"
categories:
  - "sveltekit"
  - "markdown"

coverImage: "/images/hephantan.jpeg"
coverWidth: 16
coverHeight: 9

excerpt: Đây là bài viết về hệ phân tán.
---

Hãy cùng tìm hiểu 1 số phần về hệ thống phân tán nào !!!

## 🌐 Hệ thống phân tán là gì?

Hệ thống phân tán (Distributed System) là tập hợp các máy tính độc lập, kết nối với nhau qua mạng để phối hợp làm việc như một hệ thống thống nhất. Các thành phần trong hệ thống phân tán chia sẻ tài nguyên, thực hiện đồng bộ và phục vụ người dùng cuối một cách mượt mà, ẩn đi sự phức tạp bên dưới.

---


## 🛠️ Các ứng dụng của hệ thống phân tán

- **Dịch vụ web & cloud (AWS, Google Cloud)**
- **Ứng dụng mạng xã hội (Facebook, Instagram)**
- **Thương mại điện tử (Shopee, Tiki, Lazada)**
- **Ứng dụng tài chính (Internet Banking, ví điện tử)**
- **IoT và Smart Devices (nhà thông minh, xe tự lái)**

---


## 🔑 Các khái niệm chính của hệ thống phân tán

- **Scalability**: Khả năng mở rộng.
- **Fault Tolerance**: Khả năng chịu lỗi.
- **Availability**: Khả năng sẵn sàng phục vụ.
- **Transparency**: Tính trong suốt.
- **Concurrency**: Tính đồng thời.
- **Parallelism**: Xử lý song song.
- **Openness**: Tính mở, dễ tích hợp.
- **Vertical Scaling**: Mở rộng tài nguyên cho 1 máy chủ.
- **Horizontal Scaling**: Mở rộng số lượng máy chủ.
- **Load Balancer**: Thiết bị cân bằng tải.
- **Replication**: Sao lưu và đồng bộ dữ liệu.


#### 💡 Ví dụ thực tế: Shopee

Trong hệ thống thương mại điện tử Shopee:

- **Scalability**: Hệ thống dễ mở rộng vào ngày sale.
- **Fault Tolerance**: Server chính hỏng, hệ thống phụ tiếp quản.
- **Availability**: App luôn sẵn sàng 24/7.
- **Transparency**: Người dùng không biết họ đang được phục vụ bởi nhiều server khác nhau.
- **Concurrency**: Hàng triệu người cùng đặt hàng.
- **Parallelism**: Xử lý thanh toán, tồn kho, đơn hàng cùng lúc.
- **Openness**: Tích hợp ví Momo, ZaloPay, vận chuyển GHTK.
- **Vertical Scaling**: Server database được nâng RAM, CPU.
- **Horizontal Scaling**: Thêm nhiều server ứng dụng vào cluster.
- **Load Balancer**: Phân luồng truy cập đều qua các server.
- **Replication**: Dữ liệu đơn hàng sao lưu đa vùng miền.

---

## 🏗️ Kiến trúc của hệ thống phân tán

### 1. **Client-Server**

> Mô hình truyền thống, nơi **máy khách (Client)** gửi yêu cầu và **máy chủ (Server)** phản hồi.

**Ví dụ**:
- Website trường đại học: sinh viên gửi yêu cầu tra cứu điểm (client), server xử lý và trả kết quả.
- Gmail: trình duyệt là client, server Google phản hồi email.

---

### 2. **Peer-to-Peer (P2P)**

> Mỗi nút trong mạng đều có thể vừa làm client vừa làm server. Không có server trung tâm.

**Ví dụ**:  
- BitTorrent: chia sẻ file giữa người dùng.
- Blockchain (Bitcoin, Ethereum): các nút đều xử lý và lưu dữ liệu.

---

### 3. **Microservices**

> Ứng dụng được chia nhỏ thành nhiều dịch vụ độc lập, mỗi dịch vụ thực hiện 1 chức năng riêng.

**Ví dụ**:  
- Netflix: mỗi phần như thanh toán, phát video, quản lý người dùng là một microservice.
- Shopee: service đơn hàng, ví điện tử, vận chuyển, tìm kiếm.

---

### 4. **Event-Driven Architecture**

> Các thành phần trong hệ thống giao tiếp bằng cách phát và xử lý sự kiện.

**Ví dụ**:  
- Hệ thống thông báo của Facebook: khi ai đó like ảnh, hệ thống phát sự kiện → trigger thông báo.
- Đặt hàng Lazada: sự kiện đặt hàng phát sinh, các service thanh toán, kho hàng, vận chuyển lần lượt được gọi.

---

### 5. **Lambda Architecture**

> Kiến trúc kết hợp xử lý dữ liệu real-time (stream) và batch (theo lô) để đảm bảo vừa nhanh vừa chính xác.

**Ví dụ**:  
- Hệ thống thống kê video YouTube: xử lý view theo thời gian thực (real-time), đồng thời tổng hợp báo cáo hàng ngày (batch).
- Hệ thống fraud detection của ngân hàng: kết hợp dòng dữ liệu giao dịch thật thời và batch data để phát hiện gian lận.

---

### 6. **Serverless Architecture**

> Không cần quản lý server – chỉ cần viết function, hạ tầng do cloud tự lo.

**Ví dụ**:  
- AWS Lambda: tự động chạy code khi có sự kiện (upload ảnh, gửi email).
- Ứng dụng web tĩnh sử dụng Netlify Functions.

---

### 7. **Edge Computing**

> Dữ liệu được xử lý gần nơi nó được tạo ra (gần người dùng), thay vì gửi về server trung tâm.

**Ví dụ**:  
- Xe tự lái Tesla: xử lý cảm biến ngay trên xe để phản ứng kịp thời.
- Ứng dụng nhà thông minh (Google Nest): xử lý giọng nói hoặc tín hiệu ánh sáng ngay tại thiết bị.

---



End