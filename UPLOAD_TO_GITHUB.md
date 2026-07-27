# Đưa repo lên GitHub

## Cách dùng GitHub CLI

```bash
git init
git add .
git commit -m "chore: initialize Antigravity training repository"
git branch -M main
gh repo create van-thcs-digital-store --private --source=. --remote=origin --push
```

## Cách dùng Git thuần

1. Tạo repository trống trên GitHub, không chọn tạo README.
2. Chạy:

```bash
git init
git add .
git commit -m "chore: initialize Antigravity training repository"
git branch -M main
git remote add origin <GITHUB_REPOSITORY_URL>
git push -u origin main
```

## Mở bằng Antigravity

Mở workspace tại thư mục repo rồi dùng prompt trong `docs/prompts/00-bootstrap.md`.
