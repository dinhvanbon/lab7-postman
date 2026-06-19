# 🧪 BÁO CÁO LAB 7: KIỂM THỬ API TỰ ĐỘNG VỚI APACHE POSTMAN

## 📋 Thông Tin Sinh Viên

| Thành phần | Thông tin chi tiết |
| :--- | :--- |
| **Họ và tên** | đinh văn bốn  |
| **Mã số sinh viên (MSSV)** | 22010067 |
| **Môn học** | Kiểm thử phần mềm |
| **Hệ thống API thử nghiệm** | `jsonplaceholder.typicode.com` |
| **Kết quả tổng quát** | **15 / 15 Tests Passed (Thành công 100%) ✅** |

---

## 1. Giới Thiệu Về Công Cụ Postman

**Apache Postman** là nền tảng hàng đầu hiện nay phục vụ việc phát triển, quản lý và kiểm thử tự động hệ thống API. Công cụ giúp kỹ sư QA mô phỏng toàn diện các yêu cầu dữ liệu (HTTP Requests) từ phía máy khách gửi lên hệ thống máy chủ, ghi nhận kết quả phản hồi (Responses) và xác thẩm tính toàn vẹn của dữ liệu một cách tự động thông qua các kịch bản lập trình mã nguồn.

### Các phân hệ cốt lõi được áp dụng trong bài Lab:
* **Request Builder:** Khu vực cấu hình phương thức truyền tải (Method), đường dẫn đích (URL), cấu trúc định danh Headers và nội dung đóng gói gửi đi (Body).
* **Response Viewer:** Phân khu hiển thị trực quan mã trạng thái hệ thống trả về (Status Code), thời gian xử lý lệnh (Response Time) và định dạng dữ liệu (JSON/XML).
* **Test Scripts:** Phân hệ viết mã kiểm thử tự động bằng ngôn ngữ lập trình JavaScript nhằm xác minh tính chính xác của dữ liệu trả về mà không cần kiểm tra thủ công.
* **Collections:** Thư mục quản lý khoa học, cho phép nhóm các yêu cầu API lại theo các module tính năng logic.
* **Environments:** Quản lý tập trung các biến số môi trường (như URL nền, khóa bảo mật) để chuyển đổi linh hoạt khi chạy thử nghiệm.

---

## 2. Chi Tiết Kịch Bản Kiểm Thử & Kiểm Tra Tự Động (Test Scripts)

### 2.1 Phương thức GET — Lấy danh sách toàn bộ bài viết
* **Endpoint:** `https://jsonplaceholder.typicode.com/posts`
* **Mã trạng thái trả về:** `200 OK` (Thời gian phản hồi: 342 ms | Dung lượng gói tin: 29.5 KB)

**Kịch bản kiểm thử tự động (Test Script):**
```javascript
pm.test("Status code is 200", function() {
  pm.response.to.have.status(200);
});

pm.test("Response is an array", function() {
  const jsonData = pm.response.json();
  pm.expect(jsonData).to.be.an('array');
});

pm.test("Array has 100 items", function() {
  const jsonData = pm.response.json();
  pm.expect(jsonData.length).to.eql(100);
});
