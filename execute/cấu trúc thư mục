# Tạo cấu trúc thư mục cho framework POM (Page Object Model) trong IntelliJ

## 1. Cấu trúc thư mục đề xuất (tree)
```pqsql
my-automation-project
├── pom.xml
├── testng.xml
├── src
│   ├── main
│   │   └── java
│   │       └── com/yourcompany/project      (optional helper code)
│   └── test
│       ├── java
│       │   └── com/yourcompany/project
│       │       ├── base
│       │       │   └── BaseTest.java
│       │       ├── pages
│       │       │   └── LoginPage.java
│       │       ├── tests
│       │       │   └── LoginTest.java
│       │       ├── utils
│       │       │   └── WaitUtil.java
│       │       └── listeners
│       │           └── TestListener.java
│       └── resources
│           ├── config.properties
│           ├── testdata
│           │   └── users.csv
│           └── log4j2.xml
├── drivers/               (ignored by git; optional local drivers)
└── reports/               (output folder for HTML reports)
```

## 2. Tạo folder trong IntelliJ (UI)
- Mở Project view (View → Tool Windows → Project)
- Chuột phải vào src/test → New → Directory → tạo java và resources nếu chưa có
- Trong src/test/java tạo package: chuột phải → New → Package → nhập com.yourcompany.project
- Bên trong package tạo các package con: base, pages, tests, utils, listeners (chuột phải → New → Package).
- Chuột phải vào src/test/resources → New → Directory → tạo testdata (và file config.properties, log4j2.xml ...).
- Đánh dấu loại thư mục:
  + Chuột phải src/test/java → Mark Directory as → Test Sources Root
  + Chuột phải src/test/resources → Mark Directory as → Test Resources Root
  + Tương tự cho src/main/java là Sources Root
 * Lưu ý: nếu tạo src/main/java thì code chung (utility, api clients...) nên đặt ở đó. Test code để src/test/java.

## 3. Tạo folder bằng terminal / cmd (nếu thích)
Windows CMD:
```cmd
mkdir my-automation-project
cd my-automation-project
mkdir -p src\test\java\com\yourcompany\project\{base,pages,tests,utils,listeners}
mkdir -p src\test\resources\testdata
mkdir drivers reports
```
Git Bash / Linux:
```bash
mkdir -p my-automation-project/src/test/java/com/yourcompany/project/{base,pages,tests,utils,listeners}
mkdir -p my-automation-project/src/test/resources/testdata
mkdir my-automation-project/drivers my-automation-project/reports
```
Sau đó mở IntelliJ bằng File → Open vào folder project

## 4. Gợi ý đặt tên package / files (best practice)
- Package root: com.{company}.{project} — tránh dùng automation đơn lẻ
- base — chứa BaseTest.java, DriverFactory.java
- pages — một class Page tương ứng một page/fragment (LoginPage, HomePage...)
- tests — các class test TestNG / JUnit (LoginTest, CheckoutTest...)
- utils — helper: WaitUtil, FileUtil, ExcelReader, JsonUtil
- listeners — test listeners để report, screenshot khi fail
- resources — config.properties, environment.properties, test data (CSV/JSON), log config.

## 5. Ví dụ nhanh nội dung file (minimized)
src/test/resources/config.properties
```ini
base.url=https://example.com
browser=chrome
implicit.wait=10
```
## 6. Test data & resources
- src/test/resources/testdata/users.csv — dữ liệu test dạng CSV/JSON
- src/test/resources/config.properties — cấu hình môi trường (url, browser, timeouts)
- log4j2.xml hoặc logback.xml để cấu hình logging (đặt trong resources)

## 7. Thêm folder cho Reports & drivers (không commit)
- Tạo drivers/ để chứa chromedriver/chromium nếu bạn không dùng WebDriverManager. .gitignore cần chứa drivers/ và reports/
- Tạo reports/ để output HTML reports (Allure, ExtentReports)
- Thêm .gitignore ví dụ:
```bash
/drivers/
/reports/
/target/
/.idea/
/*.iml
```

## 8. Tối ưu và tips
- Tách config theo env: config.dev.properties, config.qa.properties. Dùng biến môi trường hoặc maven profile chọn file
- Đặt các helper chung (API clients, DB helpers) vào src/main/java nếu dùng chung cho nhiều module
- Sử dụng PageFactory hoặc tạo custom Element wrapper nếu project lớn
- Dùng Maven archetype / project template nếu bạn tạo nhiều project giống nhau
