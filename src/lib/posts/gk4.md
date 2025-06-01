## Yêu cầu chức năng và phi chức năng hệ thống phân tán

- **Fault Tolerance**  
  Hệ thống phải có khả năng tiếp tục hoạt động khi một nút hoặc quá trình bị lỗi mà không làm hỏng toàn bộ hệ thống.

- **Distributed Communication**  
  Các nút/quá trình trong hệ thống phải giao tiếp với nhau qua các giao thức mạng thực tế như HTTP, gRPC, messaging, v.v.  
  Hệ thống phải hoạt động trên nhiều máy, không chỉ chạy trên một máy duy nhất.

- **Sharding hoặc Replication**  
  Hệ thống phải thực hiện một trong hai thao tác:  
  - Phân mảnh dữ liệu (chia dữ liệu theo khóa)  
  - Hoặc sao chép dữ liệu giữa các nút (Replication)

- **Simple Monitoring / Logging**  
  Hệ thống phải cung cấp khả năng giám sát đơn giản, ví dụ như nhật ký (logs), đầu ra CLI hoặc bảng điều khiển đơn giản.

- **Basic Stress Test**  
  Thực hiện kiểm tra tải cơ bản bằng cách mô phỏng nhiều yêu cầu, nhiều khách hàng, và quan sát hành vi của hệ thống.
