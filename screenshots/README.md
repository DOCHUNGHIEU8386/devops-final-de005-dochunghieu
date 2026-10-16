# Hướng dẫn chụp ảnh minh chứng (Screenshots)

Thư mục này dùng để lưu trữ các ảnh chụp màn hình minh chứng cho bài thi DevOps Final - Đề 005.

### Danh sách ảnh cần nộp:

1. **`01-actions.png`**:
   - Chụp giao diện GitHub Actions sau khi push lên branch `main`.
   - Hiển thị pipeline CI/CD chạy thành công cả 2 jobs: `build` (Build & Test) và `deploy` (Deploy lên server).

2. **`02-ghcr.png`**:
   - Chụp giao diện GitHub Packages (GHCR) của repository.
   - Hiển thị package `app` đã được push lên với 2 tags:
     + Commit SHA (ví dụ: `a1b2c3d...`)
     + `latest`

3. **`03-compose-ps.png`**:
   - Chụp màn hình terminal trên server (hoặc máy local) khi chạy lệnh:
     ```bash
     docker compose --env-file student.env ps
     ```
   - Hiển thị đầy đủ 3 services đang hoạt động:
     + `app` (Up / running)
     + `mysql` (Up / healthy)
     + `nginx` (Up / running, port `8237->80/tcp`)

4. **`04-website.png`**:
   - Chụp màn hình trình duyệt (hoặc curl) truy cập vào URL:
     `http://<SERVER_IP>:8237/api/employees`
   - Hiển thị danh sách 8 nhân viên dạng JSON.

> **Lưu ý quan trọng**: Không chụp hoặc để lộ các thông tin nhạy cảm như SSH Private Key, password thực tế trong ảnh minh chứng.
