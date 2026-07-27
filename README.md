# Văn THCS Digital Store — Antigravity Agent Kit

Repo ngữ cảnh và starter code dành cho Google Antigravity xây dựng website bán tài liệu Ngữ văn THCS theo mô hình tối giản:

**Facebook → trang sản phẩm → nhập email/số điện thoại → payOS → gửi link tải tự động.**

## Mục tiêu MVP

- Không đăng ký tài khoản khách hàng.
- Không giỏ hàng ở phiên bản đầu.
- Mỗi đơn hàng chỉ mua một sản phẩm.
- Thanh toán qua payOS.
- Webhook là nguồn xác nhận thanh toán chính thức.
- Tài liệu được giao bằng link ký số, có thời hạn và giới hạn lượt tải.
- Người bán có trang quản trị tối giản để xem sản phẩm, đơn hàng và gửi lại email.

## Repo này dùng như thế nào?

1. Tạo một repository GitHub mới.
2. Giải nén toàn bộ nội dung repo này và push lên GitHub.
3. Mở thư mục bằng Antigravity.
4. Yêu cầu Agent đọc theo thứ tự:
   - `AGENTS.md`
   - `docs/01-product-requirements.md`
   - `docs/02-user-flows.md`
   - `docs/03-architecture.md`
   - `docs/06-definition-of-done.md`
   - `TASKS.md`
5. Bắt đầu bằng prompt trong `docs/prompts/00-bootstrap.md`.

## Lệnh kiểm tra hiện có

```bash
npm install
npm test
npm run typecheck
```

Starter code hiện chỉ chứa domain model đơn hàng và test vòng đời đơn hàng. Antigravity sẽ xây ứng dụng Next.js theo từng task, không được tạo toàn bộ hệ thống trong một lần.

## Repo tham khảo

- Vercel Next.js Commerce: chỉ tham khảo cách tổ chức storefront, không copy toàn bộ vì quá phức tạp cho MVP.
- payOS Node SDK: nguồn chuẩn cho tạo payment link và xác minh webhook.

## Nguyên tắc vận hành Agent

- Explore → Plan → Implement → Test → Report.
- Mỗi task chỉ thay đổi phạm vi nhỏ.
- Không được đánh dấu hoàn thành nếu test/typecheck chưa chạy.
- Không commit secret, API key, file tài liệu thật hoặc link tải công khai.
