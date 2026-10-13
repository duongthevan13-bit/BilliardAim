# Billiard Aim Trainer

Công cụ luyện ngắm bi-a: vẽ đường ngắm và phản xạ thành băng (góc tới = góc phản xạ) lên bàn thực tế qua camera hoặc game offline cá nhân.

Không dùng cho game trực tuyến nhiều người chơi.

## Giai đoạn
1. **Khung dự án (bản này):** foreground service MediaProjection, overlay trong suốt, thu khung hình trên luồng nền, luồng xin quyền.
2. Phát hiện khung bàn và bi trắng (OpenCV, HSV, tâm và bán kính từ 4 điểm biên, perspective transform).
3. Phản xạ thành băng và vẽ đường ngắm, kéo tay chọn hướng.

## Chạy thử
1. Mở thư mục bằng Android Studio (Koala trở lên), để IDE tự đồng bộ Gradle và tạo wrapper.
2. Chạy trên máy thật (MediaProjection không ổn định trên emulator).
3. Nhấn "Bắt đầu": cấp quyền hiển thị trên ứng dụng khác, thông báo, rồi đồng ý thu màn hình.
4. Dòng chữ "Overlay OK" màu cam ở góc trên trái cho biết lớp phủ đã hoạt động.

## Lấy file APK
- **Android Studio:** Build > Build Bundle(s) / APK(s) > Build APK(s). File nằm ở `app/build/outputs/apk/debug/app-debug.apk`.
- **GitHub Actions:** đẩy thư mục này lên một repo GitHub (nhánh `main`), vào tab Actions > "Build debug APK" > tải artifact `BilliardAim-debug-apk`.
- Cài lên máy: chép APK sang điện thoại, cho phép cài từ nguồn không xác định.

## Lưu ý
- Android 14+: `startForeground` đúng type phải gọi trước `getMediaProjection`, và `registerCallback` trước `createVirtualDisplay`. Mã đã tuân theo.
- MediaProjection chụp cả overlay. Đường kẻ dùng màu cam, tách khỏi dải HSV của bi trắng.
- Ứng dụng tôn trọng cờ bảo mật màn hình hệ thống, không cố vượt FLAG_SECURE.
