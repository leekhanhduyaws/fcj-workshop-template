---
title: "Demo Ứng Dụng"
date: 2026-07-21
weight: 3
chapter: false
pre: "<b>5.7.3. </b>"
---

Sau khi VPC, RDS, EC2, S3 và Cognito đã được kết nối đầy đủ, bước này sẽ chứng minh ứng dụng FlashLearn thực sự chạy được từ đầu đến cuối trên Cloud, trước khi chuyển sang bước dọn dẹp tài nguyên.

---

## 1. Đăng ký & Đăng nhập (Amazon Cognito)

<!-- Thay bằng ảnh chụp/GIF của bạn -->
![Luồng đăng ký và đăng nhập](/images/5-Workshop/5.7-demo/register-login.gif)

1. Mở `http://<EC2-Public-IP>:5000`
2. Nhấn **Sign In** → được chuyển tới Cognito Hosted UI
3. Đăng ký tài khoản mới → xác nhận mã gửi qua email
4. Đăng nhập thành công và quay lại FlashLearn

---

## 2. Tạo bộ Flashcard

![Tạo deck](/images/5-Workshop/5.7-demo/create-deck.gif)

Tạo một deck Anh - Việt mới và thêm vài flashcard.

---

## 3. Gắn ảnh minh họa cho flashcard (Amazon S3)

![Upload ảnh flashcard](/images/5-Workshop/5.7-demo/upload-image.gif)

Upload ảnh minh họa cho một thẻ và xác nhận ảnh được phục vụ từ S3 bucket (kiểm tra URL ảnh / S3 console để chứng minh ảnh không lưu trên EC2).

---

## 4. Luyện tập với Spaced Repetition

![Chế độ luyện tập](/images/5-Workshop/5.7-demo/practice.gif)

Ôn tập một deck bằng thuật toán Spaced Repetition và cho thấy ngày ôn tập tiếp theo được cập nhật.

---

## 5. Chế độ Battle (Real-time, SignalR)

![Chế độ Battle](/images/5-Workshop/5.7-demo/battle.gif)

Mở hai phiên trình duyệt (hoặc hai tài khoản), bắt đầu battle và cho thấy cả hai bên cập nhật theo thời gian thực.

---

## 6. Video Demo Toàn Bộ (Tùy chọn)

<video controls width="100%" src="/videos/flashlearn-demo.mp4"></video>

---

## Kết quả

Sau bước này, bạn đã chứng minh được:
- Ứng dụng deploy trên EC2 truy cập được và hoạt động bình thường từ trình duyệt
- Xác thực qua Cognito hoạt động đầy đủ
- Ảnh flashcard thực sự được lưu và phục vụ từ S3
- Các tính năng real-time (SignalR) hoạt động đúng trên môi trường Cloud
