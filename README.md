# KPI School

Web app theo dõi KPI cho nhà trường. Mở `index.html` bằng trình duyệt để sử dụng ngay.

## Có sẵn

- Tạo, sửa, xóa chỉ tiêu; trọng số, hạn hoàn thành, người phụ trách và ghi chú.
- Tự tính điểm hoàn thành theo trọng số, cảnh báo quá hạn, lọc/tìm kiếm và báo cáo theo đơn vị.
- Gắn liên kết minh chứng từ Google Drive cho từng chỉ tiêu.
- Xuất toàn bộ dữ liệu ra CSV; dữ liệu tạm thời được lưu cục bộ trên trình duyệt.

## Phương án triển khai chính thức

Khuyến nghị dùng **Cloud Firestore** (thuộc Firebase) làm cơ sở dữ liệu chính, còn **Google Drive** chỉ lưu các tệp minh chứng. Cách này hỗ trợ nhiều người đồng thời cập nhật, phân quyền và có lịch sử thay đổi; Drive không phù hợp làm cơ sở dữ liệu KPI do khó truy vấn và không có giao dịch dữ liệu.

Để đưa lên Firestore cần cung cấp/tạo:

1. Một dự án Firebase, bật Authentication với tài khoản Google và tạo Cloud Firestore ở chế độ production.
2. Danh sách tài khoản/nhóm được phép theo vai trò: quản trị, tổ trưởng, giáo viên chỉ xem/cập nhật.
3. Thư mục Google Drive dùng chung cho minh chứng và quy ước quyền truy cập nội bộ.
4. Cấu trúc dữ liệu đề xuất: `kpis/{kpiId}` (title, unit, ownerId, weight, dueDate, progress, status, evidenceUrl, note, createdAt, updatedAt); `users/{uid}` (name, role, units).

Không đưa khóa quản trị Firebase hoặc khóa Google Drive vào mã nguồn trình duyệt. Cấu hình web Firebase (API key công khai) có thể đặt trong môi trường triển khai; quyền truy cập phải được bảo vệ bằng Firebase Security Rules.
