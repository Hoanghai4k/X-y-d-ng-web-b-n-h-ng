# TASKS — Thực hiện theo thứ tự

## Phase 0 — Baseline

- [ ] T-001 Khảo sát repo và lập implementation plan.
- [ ] T-002 Scaffold Next.js App Router TypeScript strict.
- [ ] T-003 Chọn ORM, tạo ADR và PostgreSQL local setup.
- [ ] T-004 Thiết lập lint, test, typecheck và CI.

## Phase 1 — Catalog

- [ ] T-101 Product schema + migration + seed.
- [ ] T-102 Trang danh sách sản phẩm mobile-first.
- [ ] T-103 Trang chi tiết sản phẩm theo slug.
- [ ] T-104 Admin CRUD sản phẩm tối giản.

## Phase 2 — Checkout

- [ ] T-201 Order schema và state transition tests.
- [ ] T-202 Form email/confirm email/phone.
- [ ] T-203 Server-side create order.
- [ ] T-204 payOS adapter và create payment link.
- [ ] T-205 Return/cancel pages không tự xác nhận payment.

## Phase 3 — Webhook

- [ ] T-301 Webhook event schema + dedup constraint.
- [ ] T-302 Verify payOS webhook.
- [ ] T-303 Atomic order payment reconciliation.
- [ ] T-304 Idempotency integration tests.
- [ ] T-305 Payment audit/admin view.

## Phase 4 — Delivery

- [ ] T-401 Private storage adapter.
- [ ] T-402 Secure delivery token service.
- [ ] T-403 Download endpoint with expiry/limit.
- [ ] T-404 Email adapter and template.
- [ ] T-405 Delivery retry + resend admin action.

## Phase 5 — Verification

- [ ] T-501 Playwright happy path using mocked provider adapter.
- [ ] T-502 Webhook replay/security tests.
- [ ] T-503 Mobile UI verification screenshots.
- [ ] T-504 Deployment runbook and production checklist.
