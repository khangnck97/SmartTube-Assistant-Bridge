# SmartTube Assistant Bridge

Bản rút gọn theo cơ chế VietMITV-v17: giữ Google TV/Google Assistant làm Assistant, dùng ADB để đọc log của Katniss và chuyển truy vấn sang SmartTube. Đã bỏ phần kênh/TV.

## Cơ chế
1. Kết nối ADB nội bộ `127.0.0.1:5555`.
2. Cấp `WRITE_SECURE_SETTINGS` + overlay app-op cho app.
3. Giữ `com.google.android.katniss` làm role Assistant.
4. Đọc `logcat -s katniss_interactor_StreamingTextView:I`.
5. Khi thấy truy vấn trong dấu ngoặc `(...)`, force-stop Katniss và mở SmartTube `com.teamsmart.videomanager.tv` bằng `SearchLauncherActivity`.

VietMITV v17 chứa chính các chuỗi/lệnh tương ứng, gồm `pm enable ...katniss`, `pm grant ...WRITE_SECURE_SETTINGS`, `appops ...SYSTEM_ALERT_WINDOW`, role Assistant và bộ lọc logcat nói trên.

## Lưu ý
Thiết bị phải có ADB TCP nội bộ trên cổng 5555 và cho phép khóa ADB của ứng dụng. Không phải mọi ROM Android TV đều mở localhost:5555; khi đó cần bật Wireless/Network debugging hoặc ADB theo cách của ROM.

SmartTube phải được cài với package `com.teamsmart.videomanager.tv`.
