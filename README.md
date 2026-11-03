# Bài 2: Xử lý sự cố Cache và Phiên đăng nhập trong doanh nghiệp

## Phần 1: Phân tích

### CSS không cập nhật

- Do **Browser Cache**: trình duyệt đã lưu file CSS cũ trên máy.
- Khi bấm F5, trình duyệt vẫn đọc file CSS cũ từ bộ nhớ đệm thay vì tải file mới từ server, nên nút "Thanh toán" vẫn hiện màu xanh cũ.

### Phiên đăng nhập bị mất khi đóng trình duyệt

- Cookie đăng nhập của An là **Session Cookie**: mã nguồn không có thuộc tính `Max-Age` hay `Expires`, nên trình duyệt coi đây là dữ liệu tạm thời và xóa ngay khi đóng trình duyệt.
- **Persistent Cookie** có `Max-Age` hoặc `Expires`, được lưu trên ổ đĩa và giữ đến ngày hết hạn, nên cần dùng loại này để duy trì đăng nhập.

| Tiêu chí | Session Cookie | Persistent Cookie |
|---|---|---|
| Thuộc tính thời hạn | Không có `Max-Age`/`Expires` | Có `Max-Age` hoặc `Expires` |
| Khi đóng trình duyệt | Bị xóa | Vẫn còn đến khi hết hạn |

## Phần 2: Sửa lỗi

1. **Hard Reload:** bấm **Ctrl + F5** (hoặc **Ctrl + Shift + R**) để buộc trình duyệt bỏ qua cache của trang hiện tại và tải lại file CSS mới nhất, không cần xóa toàn bộ lịch sử web.
2. **Đặt thời hạn cho cookie:** thêm `Max-Age` hoặc `Expires` vào cookie để chuyển thành Persistent Cookie, ví dụ:

```http
Set-Cookie: session_id=abc123; Max-Age=604800; Path=/
```
