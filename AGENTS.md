# AGENTS.md — Luật bắt buộc của dự án

## 1. Bối cảnh sản phẩm

Đây là website bán tài liệu số Ngữ văn THCS. Khách hàng chủ yếu đến từ bài đăng và nhóm Facebook. Website phải giảm tối đa số bước mua hàng.

Luồng chuẩn:

1. Khách mở đúng trang sản phẩm từ Facebook.
2. Khách xem mô tả và bản xem trước.
3. Khách nhập email, xác nhận email và số điện thoại.
4. Hệ thống tạo đơn `PENDING` và payment link payOS.
5. Khách thanh toán.
6. Backend nhận webhook, xác minh chữ ký, kiểm tra số tiền và cập nhật đơn `PAID` theo cách idempotent.
7. Hệ thống phát hành download grant và gửi email.
8. Khách tải file bằng link ký số có thời hạn.

## 2. Phạm vi MVP bắt buộc

- Không có customer account/password.
- Không có social login.
- Không có cart.
- Một checkout tương ứng một sản phẩm.
- Tiền tệ chỉ dùng VND, số tiền lưu kiểu số nguyên.
- Admin tối giản, có xác thực riêng.
- Có chức năng gửi lại email giao tài liệu.

## 3. Công nghệ mặc định

- Next.js App Router + TypeScript strict.
- PostgreSQL.
- ORM: Prisma hoặc Drizzle, chỉ chọn một và ghi ADR.
- payOS Node SDK cho thanh toán.
- Resend hoặc SMTP adapter cho email; business logic không phụ thuộc trực tiếp provider.
- Private object storage hỗ trợ signed URL.
- Vitest cho unit test; Playwright cho happy-path E2E khi UI đã sẵn sàng.

Không tách FastAPI/microservice trong MVP nếu không có ADR được chủ dự án duyệt.

## 4. Quy tắc nghiệp vụ bất biến

- `returnUrl` không được dùng để xác nhận đã thanh toán.
- Chỉ webhook payOS đã xác minh mới được chuyển đơn sang `PAID`.
- Webhook phải idempotent; nhận lại cùng sự kiện không gửi email hoặc cấp quyền tải trùng.
- Phải so khớp `orderCode`, `amount`, trạng thái hiện tại và sản phẩm.
- Không cho tải file trực tiếp bằng public URL.
- Download token không chứa đường dẫn storage bí mật.
- Không log API key, checksum key, token tải hoặc dữ liệu nhạy cảm đầy đủ.
- Không nhận trạng thái thanh toán từ client.
- Email sai không được sửa âm thầm sau thanh toán; phải có quy trình admin lưu audit.

## 5. Quy ước trạng thái đơn hàng

Các trạng thái hợp lệ:

- `PENDING`
- `PAID`
- `DELIVERY_PENDING`
- `DELIVERED`
- `EXPIRED`
- `CANCELLED`
- `REFUND_REVIEW`
- `REFUNDED`

Không thêm trạng thái mới nếu chưa cập nhật `docs/04-data-model.md` và test chuyển trạng thái.

## 6. Cách Agent làm việc

Với mọi task lớn hơn một file:

1. Đọc tài liệu liên quan.
2. Khảo sát code hiện tại, không sửa ngay.
3. Viết kế hoạch gồm file sẽ sửa, migration, test và rủi ro.
4. Chỉ triển khai sau khi kế hoạch rõ ràng.
5. Chạy ít nhất `npm test` và `npm run typecheck`.
6. Báo cáo file đã đổi, test đã chạy, phần chưa hoàn tất.

Không được:

- Tự thay đổi phạm vi MVP.
- Thêm auth khách hàng, cart, coupon, affiliate, chatbot hoặc AI content generation khi task không yêu cầu.
- Thay thư viện lõi chỉ vì sở thích.
- Xóa test đang fail để làm CI xanh.
- Dùng mock webhook trong production route mà không xác minh chữ ký.

## 7. Tiêu chuẩn code

- TypeScript strict; tránh `any`.
- Domain logic tách khỏi route handler và SDK bên thứ ba.
- Route handler mỏng: parse → validate → service → response.
- Validate input bằng schema.
- Mọi external side effect phải qua adapter/interface để test được.
- Lỗi trả về không làm lộ secret hoặc stack trace ở production.
- Dùng UTC trong database; hiển thị theo Asia/Ho_Chi_Minh.

## 8. Definition of Done

Một task chỉ hoàn thành khi:

- Acceptance criteria được đáp ứng.
- Có test cho nghiệp vụ quan trọng và lỗi biên.
- `npm test` pass.
- `npm run typecheck` pass.
- `.env.example` được cập nhật nếu có biến môi trường mới.
- Không có secret trong git diff.
- Tài liệu/ADR được cập nhật nếu thay đổi kiến trúc.
