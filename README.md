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
01_get_all_posts.png
2.2 Phương thức GET — Lấy thông tin một bài viết cụ thể (id = 1)
Endpoint: https://jsonplaceholder.typicode.com/posts/1

Mã trạng thái trả về: 200 OK (Thời gian phản hồi: 198 ms | Dung lượng gói tin: 292 B)

Kịch bản kiểm thử tự động (Test Script):
pm.test("Status code is 200", function() {
  pm.response.to.have.status(200);
});

pm.test("Post ID is 1", function() {
  const jsonData = pm.response.json();
  pm.expect(jsonData.id).to.eql(1);
});

pm.test("Response has required fields", function() {
  const jsonData = pm.response.json();
  pm.expect(jsonData).to.have.property('userId');
  pm.expect(jsonData).to.have.property('title');
  pm.expect(jsonData).to.have.property('body');
});
02_get_specific_post.png
2.3 Phương thức POST — Tạo mới một bản ghi bài viết
Endpoint: https://jsonplaceholder.typicode.com/posts

Mã trạng thái trả về: 201 Created (Thời gian phản hồi: 289 ms | Dung lượng gói tin: 115 B)

Dữ liệu yêu cầu gửi lên (Request Body - định dạng JSON raw):

JSON
{
  "title": "Bài viết kiểm thử với Postman",
  "body": "Nội dung được tạo bằng Postman trong Lab 7",
  "userId": 1
}
03_post_new_article.png
2.4 Phương thức PUT — Cập nhật toàn bộ nội dung của bài viết (id = 1)
Endpoint: https://jsonplaceholder.typicode.com/posts/1

Mã trạng thái trả về: 200 OK (Thời gian phản hồi: 215 ms | Dung lượng gói tin: 108 B)

Dữ liệu yêu cầu cập nhật (Request Body - định dạng JSON raw):

JSON
{
  "id": 1,
  "title": "Tiêu đề đã được cập nhật",
  "body": "Nội dung bài viết đã được thay đổi hoàn toàn",
  "userId": 1
}
04_put_update_article.png
2.5 Phương thức PATCH — Cập nhật một phần thuộc tính bài viết (id = 1)
Endpoint: https://jsonplaceholder.typicode.com/posts/1

Mã trạng thái trả về: 200 OK (Thời gian phản hồi: 176 ms | Dung lượng gói tin: 136 B)

Dữ liệu yêu cầu sửa đổi (Request Body - định dạng JSON raw):

JSON
{
  "title": "Chỉ cập nhật tiêu đề bằng PATCH"
}
05_patch_partial_update.png
2.6 Phương thức DELETE — Xóa bỏ bản ghi bài viết khỏi hệ thống (id = 1)
Endpoint: https://jsonplaceholder.typicode.com/posts/1

Mã trạng thái trả về: 200 OK (Thời gian phản hồi: 187 ms | Dung lượng gói tin: 2 B)

Kịch bản kiểm thử tự động (Test Script):

JavaScript
pm.test("Status code is 200", function() {
  pm.response.to.have.status(200);
});

pm.test("Response body is empty object", function() {
  const jsonData = pm.response.json();
  pm.expect(jsonData).to.eql({});
});
06_delete_article.png
3. Cấu Hình Biến Môi Trường (Environment Variables)Việc sử dụng Environment Variables giúp tối ưu hóa kịch bản kiểm thử, dễ dàng bảo trì hệ thống khi thay đổi cổng Domain máy chủ endpoint mà không cần sửa đổi thủ công từng Request một.Cấu hình phân hệ môi trường mang tên Lab7-Env:Biến số base_url (Initial & Current Value): https://jsonplaceholder.typicode.comBiến số post_id (Initial & Current Value): 1Áp dụng URL động linh hoạt trong Postman:Cú pháp sử dụng: {{base_url}}/posts/{{post_id}} $\rightarrow$ Khi hệ thống thực thi sẽ tự động hiểu chính xác là đường dẫn: https://jsonplaceholder.typicode.com/posts/1
07_environment_variables.png
4. Quản Lý Cấu Trúc Collection & Kết Quản Chạy Tự Động (Runner)
Toàn bộ các yêu cầu kiểm thử đơn lẻ được đóng gói và phân tầng thư mục logic trong một Collection mang tên Lab7 - API Testing:

Lab7 - API Testing (Collection)
├── 📁 GET Requests
│   ├── Lấy tất cả bài viết
│   └── Lấy bài viết id=1
├── 📁 POST Requests
│   └── Tạo bài viết mới
├── 📁 PUT & PATCH
│   ├── Cập nhật toàn bộ (PUT)
│   └── Cập nhật 1 phần (PATCH)
└── 📁 DELETE
    └── Xóa bài viết
📈 Thống kê hiệu năng thực thi từ Collection Runner:
Tổng số lượng Request thực thi tự động trong chuỗi liên hoàn: 6 Requests.

Tổng số kịch bản kiểm thử đạt tiêu chuẩn (Passed): 15 Tests thành công.

Tổng số kịch bản kiểm thử không đạt tiêu chuẩn (Failed): 0 lỗi phát sinh.

Tổng thời gian xử lý toàn trình (Duration): 1.3 giây.
08_collection_runner.png
5. Bảng Thống Kê Tổng Kết Kết Quả Kiểm Thử (Summary Table)
09_summary_results.png
STTPhương thứcĐường dẫn kiểm thử (Endpoint)Mã trạng thái (Status)Số lượng TestTrạng thái kết quả1GET/posts200 OK3 / 3✅ PASSED2GET/posts/1200 OK3 / 3✅ PASSED3POST/posts201 Created3 / 3✅ PASSED4PUT/posts/1200 OK2 / 2✅ PASSED5PATCH/posts/1200 OK2 / 2✅ PASSED6DELETE/posts/1200 OK
6. Kết Luận Bài Học Thực Hành
Sau khi hoàn tất quy trình thực hiện nội dung thực hành Lab 7, bản thân đã làm chủ được các kiến thức cốt lõi:

[x] Cài đặt thành thạo và làm quen với giao diện, cơ chế hoạt động của Apache Postman.

[x] Hiểu sâu sắc bản chất kỹ thuật, cách truyền tải tham số và ngữ cảnh áp dụng thực tế của 5 phương thức HTTP cốt lõi: GET, POST, PUT, PATCH, DELETE.

[x] Sử dụng linh hoạt ngôn ngữ JavaScript áp dụng vào phân hệ Test Scripts để thiết lập cơ chế tự động hóa kiểm định tính hợp lệ của mã lỗi và cấu trúc gói tin JSON trả về.

[x] Biết cách quản lý dự án API một cách khoa học bằng phân tầng Collections và tối ưu hóa hệ thống bằng biến môi trường Environment Variables.

[x] Khai thác tối đa sức mạnh của công cụ thông qua tính năng Collection Runner nhằm thực thi các kịch bản kiểm thử hồi quy (Regression Testing) toàn chuỗi API một cách tự động chỉ bằng một click chuột.

7. Tài Liệu Tham Khảo
Postman Official Documentation: https://learning.postman.com/docs/

Postman Test Scripts Guide: Writing test scripts in Postman

JSONPlaceholder Service: https://jsonplaceholder.typicode.com/

Video hướng dẫn thực hành học tập: Video hướng dẫn Lab 7 (YouTube)

Báo cáo được hoàn thiện nghiêm túc phục vụ cho học phần Kiểm thử phần mềm.
