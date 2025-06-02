---
title: "Deliverable 3"
date: "2025-05-31"
updated: "2025-05-31"
categories:
  - "sveltekit"
  - "markdown"

coverImage: "/images/pickleDB.png"
coverWidth: 16
coverHeight: 9

---



## Tóm Tắt Tiến Độ Dự Án: Task Manager


### 1. Các tính năng chính đã triển khai

- **Đăng ký, đăng nhập người dùng**  
  Người dùng có thể đăng ký tài khoản và đăng nhập bằng username, password (và email nếu có).

- **Quản lý và phân quyền task**  
  Người dùng có thể tạo task, gán task cho chính mình hoặc người khác.

- **Chia sẻ dữ liệu giữa các thành phần**  
  Backend (Flask + PickleDB) lưu trữ toàn bộ dữ liệu, frontend (React) giao tiếp qua REST API.

- **Giao tiếp giữa frontend và backend**  
  Qua các endpoint RESTful: đăng ký, đăng nhập, tạo/lấy/sửa/xóa task, lấy danh sách user.

- **Dashboard thống kê**  
  Hiển thị số lượng task đã tạo, được giao, và trạng thái (open, in progress, completed).

- **Xử lý lỗi cơ bản**  
  Hiển thị lỗi khi đăng nhập thất bại, hoặc thao tác không hợp lệ.

---

### 2. Phần đã hoàn thành

- Đăng ký, đăng nhập, lưu thông tin người dùng.
- Tạo, sửa, xóa, phân công task.
- Lấy danh sách task theo user.
- Dashboard thống kê task.
- Giao diện cơ bản bằng React + Tailwind CSS.
- Docker hóa backend và frontend với `docker-compose`.

---

### 3. Vấn đề đã gặp & cách giải quyết

#### Vấn đề:
- Lỗi đồng bộ dữ liệu khi phân công lại task cho user khác.
- Ghi đè dữ liệu không hợp lệ ở `assigned_user` và `created_by`.
- Backend trả về dữ liệu sai định dạng, gây lỗi phía frontend.

#### Giải pháp:
- Kiểm tra và **validate** dữ liệu ở cả frontend và backend.
- Lưu username vào **localStorage** để đồng bộ giữa các request.
- Thêm thông báo lỗi rõ ràng trên giao diện.

---

## Mã nguồn quan trọng (Code Snippets)

### 🔹 API tạo task (Flask Backend)

```python
@app.route('/task', methods=['POST'])
def create_task():
    data = request.json
    username = data.get('username')
    task_data = data.get('task')
    if not username or not task_data:
        return jsonify({"message": "Username and task required"}), 400
    task_id = str(uuid.uuid4())
    assigned_user = task_data.get('assigned_user') or username
    task = {
        "id": task_id,
        "title": task_data.get('title'),
        "description": task_data.get('description'),
        "due_date": task_data.get('due_date'),
        "status": task_data.get('status', 'open'),
        "priority": task_data.get('priority', 'low'),
        "created_by": username,
        "assigned_user": assigned_user
    }
    all_tasks = get_all_tasks()
    all_tasks.append(task)
    save_all_tasks(all_tasks)
    return jsonify({"message": "Task created", "task": task}), 201
```
### 🔹 Lấy task theo user (frontend React)

```python
useEffect(() => {
  if (!username) {
    setLoading(false);
    return;
  }
  const fetchTasks = async () => {
    try {
      const data = await getTasks(username);
      setTasks(Array.isArray(data) ? data : []);
    } catch (err) {
      setTasks([]);
    } finally {
      setLoading(false);
    }
  };
  fetchTasks();
}, [username]);

```
### 🔹 Lưu thông tin đăng nhập vào localStorage

```python
export const setToken = (tokens) => {
  if (tokens && tokens.username) {
    localStorage.setItem('username', tokens.username);
  }
  localStorage.setItem('tokens', JSON.stringify(tokens));
};
```

## Danh sách tính năng đã hoàn thành

- Đăng ký, đăng nhập người dùng.
- Tạo, sửa, xóa, phân công task.
- Lấy danh sách task theo user.
- Dashboard thống kê task.
- Xử lý lỗi cơ bản, thông báo cho người dùng.
- Docker hóa hệ thống, chạy đồng thời frontend/backend.

---

## Kế hoạch tiếp theo

- Thêm thông báo real-time khi task được giao hoặc hoàn thành.
- Bổ sung phân quyền nâng cao (chỉ người tạo hoặc người được giao mới sửa/xóa task).
- Tối ưu bảo mật (hash password, xác thực JWT nếu cần).
- Deploy được web lên server.

---

End