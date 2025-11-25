#RUN

## Step 1: Khởi động máy ảo - Android Studio
- Prepare Android Device/Emulator
- Connect your Android device or start emulator
- Enable USB debugging (for physical device)
  
## Step 2: Start Appium Server
1. Connect Appium Server
  Open Terminal/ command prompt
   ```bash
   appium
   ```
2. Verify device is connected
  Open Terminal/ command prompt
   ```bash
   adb devices
   ```
3. Appium: Start session
**Format**
{
  "platformName": "Android",
  "appium:automationName": "UiAutomator2",
  "appium:appPackage": "com.saucelabs.mydemoapp.android",
  "appium:appActivity": "com.saucelabs.mydemoapp.android.MainActivity",
  "appium:ap": "/Users/doaitran/Documents/Personal/Smart Testing Lab/mda-2.2.0-25.apk",
  "appium:noReset": true
}

_Giải thích từng giá trị_
- **platformName:** Hệ điều hành của thiết bị cần test: Android, iOS
- **appium:automationName:**: Engine tự động hóa mà Appium dùng để giao tiếp với thiết bị
  + "UiAutomator2": là framework mặc định và phổ biến nhất cho Android từ Android 6.0 trở lên
  + iOS: lựa chọn khác có thể là "Espresso", "UiAutomator", "XCUITest"
- **appium:appPackage:** Package name (tên gói ứng dụng) của app Android cần test
Ví dụ: "com.saucelabs.mydemoapp.android" → đây là tên định danh duy nhất của app trong thiết bị.
- appium:appActivity: Activity khởi đầu của ứng dụng
Ví dụ: "com.saucelabs.mydemoapp.android.MainActivity" → Appium sẽ mở trực tiếp màn hình này khi launch app.
- **appium:app:**: Đường dẫn đến file .apk (app Android) trên máy tính
→ Nếu app đã cài sẵn trên thiết bị, có thể bỏ key này đi và chỉ cần appPackage + appActivity.
- **appium:noReset:**: 
  + true nghĩa là không reset app khi khởi chạy session (app sẽ giữ nguyên trạng thái cũ: login, data, cache...)
  + false nghĩa là mỗi lần test, app sẽ reset về trạng thái mới cài
 
_Note:_ Để lấy giá trị appium:appPackage và appium:appActivity của ứng dụng đã cài trên thiết bị Android, làm theo các cách sau:
1. Mở app đã cài trên device
2. Open Terminal/ command
### Method 1: Dùng ADB command
- Precondition: đã cài ADB - Android Debug Bridge và điện thoại bật USB Debugging
1. Mở ứng dụng cần test trên điện thoại.
2. Run the following command:
   ```bash
   adb shell dumpsys window | find "mCurrentFocus"
   ```
 👉 Kết quả trả về dạng:
 mCurrentFocus=Window{123456 u0 com.example.myapp/com.example.myapp.MainActivity}
 
-> com.example.myapp → appPackage
-> com.example.myapp.MainActivity → appActivity

### Method 2: Dùng ADB + pm list
- Liệt kê toàn bộ package trên thiết bị:
```bash
adb shell pm list packages | grep myapp
```
```bash
adb shell dumpsys package com.example.myapp | grep -A 1 MAIN
```
→ sẽ thấy Activity chính (launcher).

### Method 3: Dùng Appium Inspector (nếu app đã cài)
Trong Inspector, nhập tạm appPackage và appActivity nếu biết một phần. Nếu sai, Inspector sẽ báo lỗi và log ra activity thực tế.

## Extra
**MoMo**
- Staging: mCurrentFocus=Window{1d5d3fd u0 vn.momo.platform.staging/vn.momo.platform.entry.MainActivity}
  "appium:appPackage": "vn.momo.platform.staging",
  "appium:appActivity": "vn.momo.platform.entry.MainActivity"
- UAT: vn.momo.platform.test/vn.momo.platform.entry.MainActivity}
