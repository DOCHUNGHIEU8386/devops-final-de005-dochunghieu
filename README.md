# DevOps Final – Đề 005: Quản lý nhân viên

Bộ mã nguồn cho bài thi **DevOps Fundamentals – Cuối kỳ**.
Ứng dụng hiển thị **danh sách nhân viên** lấy từ MySQL thông qua Spring Boot, trả về **dạng JSON** qua Nginx (reverse proxy).

## Thông tin sinh viên
- **Họ và tên:** Đỗ Chung Hiếu
- **Mã sinh viên:** PTIT-HN-237
- **Lớp:** D21CQCN01-B
- **Tên repository:** devops-final-de005-dochunghieu
- **Branch chính:** main

## Kiến trúc

```
Trình duyệt ── http://<IP_máy_chủ>:<APP_PORT>
    ▼
[nginx]  nginx:1.27-alpine        GET /*  → app:8080
    ▼
[app]    Spring Boot 4 (JRE 21)   GET /api/employees → mysql:3306
    ▼
[mysql]  mysql:8.0                volume mysql_data, KHÔNG public cổng mysql
```

## Cấu trúc thư mục

```
devops-final-de005-dochunghieu/
├── src/main/java/com/ptit/devops/hrm/   ← Controller, Entity, Repository
├── src/main/resources/application.properties
├── build.gradle                   ← Build ra file build/libs/app.jar
├── settings.gradle
├── Dockerfile                     ← Multi-stage build (build: Gradle JDK 21, runtime: Temurin JRE 21)
├── .dockerignore
├── nginx/default.conf             ← Reverse proxy tới app:8080
├── database/init.sql              ← Bảng employees + 8 bản ghi mẫu
├── docker-compose.yml             ← Compose app, mysql, nginx
├── .github/workflows/ci-cd.yml    ← Pipeline CI/CD: build, test, push GHCR, SSH deploy
├── student.env                    ← Cấu hình thông tin sinh viên & môi trường
├── screenshots/                   ← Ảnh minh chứng
├── submission-content/            ← Toàn bộ tệp minh chứng khi nộp bài
├── .gitignore
└── README.md
```

## API của ứng dụng

| Method | Đường dẫn | Mô tả |
|--------|-----------|-------|
| GET | `/api/employees` | Danh sách nhân viên (JSON) |

## Biến môi trường

| Biến | Ý nghĩa |
|------|---------|
| `DB_HOST`, `DB_PORT` | Địa chỉ MySQL (mặc định `mysql`, `3306`) |
| `DB_NAME`, `DB_USER`, `DB_PASSWORD` | Database và tài khoản kết nối |
| `APP_VERSION` | Phiên bản (truyền vào lúc build image, ví dụ commit SHA) |

## Chạy thử với Docker Compose

```bash
docker compose --env-file student.env up -d --build
docker compose --env-file student.env ps
curl http://localhost:8237/api/employees
docker compose --env-file student.env down
```
