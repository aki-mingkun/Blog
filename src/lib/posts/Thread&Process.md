---
title: "Tiến trình & Luồng"
date: "2025-05-05"
updated: "2025-05-05"
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/tien-trinh-va-luong.jpg"
coverWidth: 16
coverHeight: 9
excerpt: Đây là bài tìm hiểu về tiến trình và luồng.
---

## 1. Đánh giá hiệu năng hệ thống máy tính của tôi

### 1. Cấu hình phần cứng

![alt text](../../../images/system-info.png)

- **CPU**: AMD Ryzen 5 5625U with Radeon Graphics  
  - 6 nhân, 12 luồng  
  - Tốc độ ~2.3GHz  
  - Hỗ trợ **SMT (Simultaneous Multithreading)**  
 👉 Phù hợp cho đa nhiệm, lập trình, học máy, và chỉnh sửa video nhẹ

![alt text](../../../images/task-manager.png)

- **RAM**: 8GB (8192MB)  
  - Đủ cho: lướt web, lập trình, chạy IDE (VSCode, PyCharm,...)  
 ❗ Có thể thiếu nếu: mở nhiều tab Chrome, chạy máy ảo, app nặng

- **GPU**: Radeon Graphics (tích hợp)  
  - Đủ dùng cho đồ họa cơ bản, tăng tốc phần cứng  
  - Không phù hợp cho: chơi game nặng, thiết kế đồ họa 3D chuyên sâu

- **Bộ nhớ ảo (Page file)**:  
  - 9.3GB đã dùng, còn 2.5GB trống  
 👉 RAM gần đầy → cân nhắc nâng cấp

- **DirectX**: 12  
  - Hỗ trợ tốt cho các ứng dụng và game hiện đại

---

### 2. Hiệu năng tiến trình và hệ thống

- **Tiến trình tiêu biểu**:
  - Google Chrome: sử dụng ~1.5GB RAM
  - Obsidian, Discord, Phone Link, PostgreSQL, MySQL, WebView2...
 👉 Nhiều ứng dụng nền đang chạy

- **Tải CPU**: chỉ ~10%  
  - → CPU còn dư hiệu năng cho các tác vụ khác

- **Context Switching**:
  - Hệ điều hành chuyển đổi giữa các tiến trình trên 12 luồng CPU  
  - Giúp chạy đa nhiệm mượt mà hơn

---

### 3. Kết luận

- **Phù hợp với**:
  - Lập trình (Python, C++, Java, v.v.)
  - Làm việc văn phòng
  - Chạy IDE và đa nhiệm trung bình

- **Giới hạn khi**:
  - Mở quá nhiều tab Chrome hoặc app nặng
  - Chạy các tác vụ yêu cầu GPU cao (game, xử lý AI bằng GPU)

---


## 2. 12 Bài toán phổ biến trong ngành CNTT có sử dụng đa luồng / đa tiến trình

| STT | Bài toán                                 | Mô tả sử dụng đa luồng / đa tiến trình                                                   |
|-----|------------------------------------------|-------------------------------------------------------------------------------------------|
| 1   | Web Server (HTTP server)                 | Mỗi request được xử lý bằng một thread riêng (multi-threaded)                            |
| 2   | Trình duyệt web                          | Mỗi tab hoặc extension là một process riêng                                              |
| 3   | Công cụ tìm kiếm (Search Engine)         | Crawl web bằng nhiều thread song song                                                    |
| 4   | Phân tích dữ liệu lớn (Big Data ETL)     | Chia dữ liệu thành phần nhỏ xử lý bằng nhiều process                                     |
| 5   | Trí tuệ nhân tạo (AI model training)     | Dữ liệu chia batch, train bằng nhiều thread hoặc GPU                                     |
| 6   | Trò chơi điện tử (Game engine)           | Render, âm thanh, logic game chạy trên các thread khác nhau                             |
| 7   | IDE (VSCode, IntelliJ...)                | Chạy debugger, build, lint trên các thread riêng                                         |
| 8   | Phần mềm nén file                        | Chia file thành phần, nén song song                                                      |
| 9   | Phần mềm streaming video (Netflix, VLC)  | Thread cho decoding video, audio, I/O                                                    |
| 10  | Hệ thống ngân hàng                        | Mỗi giao dịch xử lý ở process riêng để đảm bảo an toàn                                   |
| 11  | Dịch máy (Machine Translation)           | Mỗi đoạn văn xử lý riêng biệt, dùng process hoặc thread tùy khối lượng dữ liệu          |
| 12  | Mô phỏng vật lý / hệ thống (Simulator)   | Mỗi vùng mô phỏng có thể dùng process hoặc thread độc lập tùy độ phân chia và tài nguyên |
---

## 3. Khi nào dùng Thread vs Process 

![alt text](<../../../images/khi nào dùng thread&process.jpg>)
---

## 4. ChatGPT training trên hệ phân tán (Distributed System) như thế nào.

### Tổng quan
- Mô hình như ChatGPT (GPT-3, GPT-4...) được huấn luyện trên hàng **ngàn GPU**.
- Dữ liệu lớn (~570GB+ sau xử lý) được phân mảnh và xử lý bằng hệ thống phân tán.
- Dùng **Data Parallelism**: mỗi GPU xử lý 1 phần dữ liệu.
- Dùng **Model Parallelism**: chia mô hình ra nhiều phần chạy song song.
- Sử dụng framework như: **PyTorch**, **DeepSpeed**, **Tensor Parallelism**, **Pipeline Parallelism**.

### Công nghệ sử dụng
- **NVIDIA A100 GPUs**
- **Tensor cores + High-speed interconnects (NVLink, Infiniband)**
- Hệ điều hành tối ưu cho HPC
- Dữ liệu phân phối qua các node trong siêu máy tính

### Nguồn tham khảo

1. [OpenAI Blog - Training GPT models](https://openai.com/research)
2. [How OpenAI Trained GPT-3](https://www.semanticscholar.org/paper/Language-Models-are-Few-Shot-Learners-Brown-Mann/0c3f0ef3b802db1e24f4b37f0f3bfa3d0a54e982)
3. [Distributed Training in PyTorch](https://pytorch.org/tutorials/intermediate/ddp_tutorial.html)
4. [DeepSpeed by Microsoft](https://www.deepspeed.ai/)

---

