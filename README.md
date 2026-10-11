# Bài 3: Đóng gói trang Web HTML tĩnh bằng Docker

## 1. Mục tiêu

- Tạo trang web HTML tĩnh.
- Sử dụng Dockerfile để đóng gói trang web vào Nginx image.
- Build Docker Image và chạy Container.
- Kiểm tra nội dung trang web thông qua cổng 8081.

## 2. Cấu trúc thư mục

```text
ex3/
├── index.html
├── Dockerfile
└── README.md
```

## 3. Nội dung index.html

```html
<h1>Hello Docker Session 09!</h1>
```

## 4. Nội dung Dockerfile

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

## 5. Build Docker Image

Lệnh thực hiện:

```bash
docker build -t my-html-app:v1 .
```

Giải thích:

- `docker build`: xây dựng Docker Image.
- `-t my-html-app:v1`: đặt tên image là `my-html-app`, tag `v1`.
- `.`: sử dụng thư mục hiện tại làm build context.

## 6. Khởi chạy Container

Lệnh thực hiện:

```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

Giải thích:

- `-d`: chạy container ở chế độ nền.
- `-p 8081:80`: ánh xạ cổng 8081 trên máy host sang cổng 80 trong container.
- `--name html-app`: đặt tên container là `html-app`.
- `my-html-app:v1`: image dùng để tạo container.

## 7. Kiểm tra kết quả

Lệnh thực hiện:

```bash
curl http://localhost:8081
```

Kết quả mong đợi:

```html
<h1>Hello Docker Session 09!</h1>
```

Nếu kết quả trả về đúng nội dung trên, trang HTML đã được phục vụ thành công bởi Nginx chạy trong Docker Container.

## 8. Kết luận

Đã tạo Docker Image `my-html-app:v1` từ image nền `nginx:alpine`, sao chép trang HTML vào thư mục phục vụ mặc định của Nginx và chạy container trên cổng 8081.

Đã kiểm tra khả năng truy cập trang web bằng lệnh curl.
