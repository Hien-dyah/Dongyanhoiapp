# Ứng dụng Quản lý Hội Đông y phường An Hội

Ứng dụng web/PWA phục vụ quản lý hội viên, hoạt động chuyên môn, báo cáo và văn bản của Hội Đông y phường An Hội.

## Công nghệ
- Giao diện web tĩnh HTML/CSS/JavaScript.
- Supabase Auth, PostgreSQL, Row Level Security và Edge Functions.
- PWA: `manifest.webmanifest`, `sw.js`, `icon.svg`.
- Tệp đính kèm lưu trong bucket riêng tư `association-private`.

## Vai trò hệ thống
- ADMIN: quản trị hệ thống, quản lý chức vụ kiêm nhiệm, bàn giao quyền ADMIN.
- EXECUTIVE: Ban Thường vụ, xem toàn Hội và quyết định cuối cùng.
- COMMITTEE: Ban Chấp hành, xem báo cáo và góp ý, không duyệt cuối.
- BRANCH_HEAD: Chi hội trưởng, kiểm tra hồ sơ và quản lý phạm vi chi hội.
- MEMBER: Hội viên, cập nhật hồ sơ của mình và gửi báo cáo.

Chức vụ kiêm nhiệm (Chủ tịch, Phó Chủ tịch, Thư ký, Kế toán, Thủ quỹ, Phụ trách chuyên môn...) được lưu tách biệt trong `positions` / `user_positions`, không tự cấp quyền hệ thống.

## Quy trình
- Hội viên đăng ký → Chi hội trưởng kiểm tra → Ban Thường vụ duyệt/từ chối.
- Báo cáo bản nháp → gửi → xem xét → góp ý/yêu cầu bổ sung → Ban Thường vụ duyệt/từ chối.
- Nhật ký thay đổi ghi lại thao tác trên dữ liệu hội viên, báo cáo và phân công chức vụ.
- Bàn giao ADMIN thực hiện qua RPC được bảo vệ, chỉ ADMIN hiện tại được gọi; sau bàn giao, quyền ADMIN của tài khoản chuyển giao được thu hồi.

## Cài đặt
1. Cấu hình Supabase URL và publishable key trong `index.html`.
2. Bật GitHub Pages cho nhánh `main`.
3. Đăng nhập bằng tài khoản ADMIN.
4. Mở Quản trị hệ thống → Khởi tạo kho tệp bảo mật để tạo bucket riêng tư.
5. Tạo/phân công chức vụ và sử dụng các phân hệ báo cáo, tin tức, công việc, văn bản.

Không đưa Supabase service-role key vào mã nguồn trình duyệt.