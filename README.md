

## Hệ thống đánh giá an toàn bảo mật – Flutter + Laravel

## 📄 FILE `README.md` HOÀN CHỈNH

```markdown
# HỆ THỐNG ĐÁNH GIÁ AN TOÀN BẢO MẬT

## 📋 TỔNG QUAN

Hệ thống đánh giá an toàn bảo mật đa nền tảng, hỗ trợ **Web, Android, iOS** với **10 role** khác nhau, **20 lĩnh vực**, **400 tiêu chí** và **~5.600 điều kiện** đánh giá.

### Thông tin dự án

| Thông tin | Giá trị |
|-----------|---------|
| **Tên dự án** | Security Evaluation System |
| **Phiên bản** | v4.0 |
| **Ngày tạo** | 2025-01-20 |
| **Backend** | Laravel 11 (PHP 8.x) |
| **Frontend Mobile** | Flutter 3.x (Dart) |
| **Database** | MySQL 8.0 |
| **Hỗ trợ** | Android 5.0+, iOS 11+ |

### 10 Role trong hệ thống

| ID | Role | Cấp độ | Mô tả |
|----|------|--------|-------|
| 1 | Dev | Thấp | Lập trình viên |
| 2 | BA | Thấp | Phân tích nghiệp vụ |
| 3 | DA | Thấp | Phân tích dữ liệu |
| 4 | HR | Thấp | Nhân sự |
| 5 | QA | Thấp | Kiểm thử chất lượng |
| 6 | SecOps | Cao | Vận hành bảo mật |
| 7 | Admin | Cao | Quản trị hệ thống |
| 8 | Auditor | Cao | Kiểm toán |
| 9 | Manager | Cao | Quản lý |
| 10 | CISO | Cao | Giám đốc an ninh thông tin |

---

## 🏗️ CẤU TRÚC DỰ ÁN

```
security_system_v4/
│
├── flutter_app/                    # Flutter mobile app
│   ├── lib/                        # Mã nguồn chính
│   ├── android/                    # Cấu hình Android
│   ├── ios/                        # Cấu hình iOS
│   ├── assets/                     # Tài nguyên
│   └── pubspec.yaml                # Dependencies
│
├── laravel_backend/                # Laravel backend API
│   ├── app/                        # Mã nguồn chính
│   ├── database/                   # Migrations, seeders
│   ├── routes/                     # API routes (v1, v2, v3)
│   ├── config/                     # Cấu hình
│   └── .env                        # Biến môi trường
│
├── database/                       # Shared database schema
│   └── schema.sql                  # Full database schema
│
└── docs/                           # Tài liệu
    ├── API_DOCS.md                 # API documentation
    ├── DEPLOYMENT.md               # Hướng dẫn triển khai
    └── USER_GUIDE.md               # Hướng dẫn sử dụng
```

---

## 📱 YÊU CẦU HỆ THỐNG

### Backend (Laravel)

| Thành phần | Yêu cầu |
|------------|---------|
| PHP | >= 8.1 |
| Composer | >= 2.x |
| MySQL | >= 5.7 hoặc 8.0 |
| Node.js | >= 16.x (cho frontend assets) |
| Redis | >= 6.x (tùy chọn cho queue) |

### Frontend (Flutter)

| Thành phần | Yêu cầu |
|------------|---------|
| Flutter | >= 3.16.x |
| Dart | >= 3.2.x |
| Android Studio | >= 2022.3 (cho Android) |
| Xcode | >= 14.x (cho iOS, chỉ trên Mac) |
| JDK | >= 11 |

---

## 🚀 CÀI ĐẶT VÀ CHẠY

### 1. Cài đặt Backend (Laravel)

```bash
# Clone dự án
git clone https://github.com/your-repo/security_system_v4.git
cd security_system_v4/laravel_backend

# Cài đặt dependencies
composer install

# Copy file .env
cp .env.example .env

# Tạo application key
php artisan key:generate

# Cấu hình database trong file .env
# DB_CONNECTION=mysql
# DB_HOST=127.0.0.1
# DB_PORT=3306
# DB_DATABASE=security_system
# DB_USERNAME=root
# DB_PASSWORD=

# Chạy migrations và seeders
php artisan migrate --seed

# Tạo storage link
php artisan storage:link

# Chạy queue worker (cho đồng bộ)
php artisan queue:work

# Chạy server
php artisan serve

# Server chạy tại: http://localhost:8000
```

### 2. Cài đặt Frontend (Flutter)

```bash
# Di chuyển vào thư mục flutter
cd ../flutter_app

# Cài đặt dependencies
flutter pub get

# Chạy code generator (nếu có retrofit/floor)
flutter pub run build_runner build --delete-conflicting-outputs

# Kết nối thiết bị hoặc mở emulator
# Android: mở Android Emulator
# iOS: mở iOS Simulator (chỉ trên Mac)

# Chạy ứng dụng
flutter run

# Chọn thiết bị:
# > flutter run -d android   # Android
# > flutter run -d ios       # iOS
# > flutter run -d chrome    # Web
```

### 3. Cấu hình Database

```sql
-- Tạo database
CREATE DATABASE security_system CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Tạo user (tùy chọn)
CREATE USER 'security_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON security_system.* TO 'security_user'@'localhost';
FLUSH PRIVILEGES;
```

---

## 🔧 CẤU HÌNH KẾT NỐI

### Cấu hình CORS (Laravel)

**`config/cors.php`**

```php
return [
    'paths' => ['api/*', 'sanctum/csrf-cookie'],
    'allowed_methods' => ['*'],
    'allowed_origins' => ['*'], // Cho phép tất cả (chỉ dùng dev)
    'allowed_headers' => ['*'],
    'supports_credentials' => true,
];
```

### Cấu hình API URL (Flutter)

**`lib/core/constants/api_constants.dart`**

```dart
class ApiConstants {
  // Android emulator: 10.0.2.2
  // iOS simulator: localhost
  // Thiết bị thật: IP máy tính
  static const String baseUrl = "http://10.0.2.2:8000/api/v3";
}
```

---

## 📡 API ENDPOINTS

### Phiên bản API

| Version | Base URL | Mô tả |
|---------|----------|-------|
| v1 | `/api/v1` | LITE (3 role, 50 tiêu chí) |
| v2 | `/api/v2` | PRO (5 role, 150 tiêu chí) |
| v3 | `/api/v3` | ENTERPRISE (10 role, 400 tiêu chí) |

### Các endpoint chính

```yaml
# Auth
POST   /api/v3/auth/login           # Đăng nhập
POST   /api/v3/auth/logout          # Đăng xuất
POST   /api/v3/auth/refresh         # Refresh token
POST   /api/v3/auth/verify-otp      # Xác thực OTP
POST   /api/v3/auth/verify-key      # Xác thực Key

# User
GET    /api/v3/user/profile         # Lấy thông tin user
PUT    /api/v3/user/profile         # Cập nhật profile
GET    /api/v3/user/employees       # Lấy danh sách nhân viên

# Evaluation
GET    /api/v3/evaluations          # Lấy danh sách đánh giá
POST   /api/v3/evaluations          # Tạo đánh giá mới
PUT    /api/v3/evaluations/{id}     # Cập nhật đánh giá
DELETE /api/v3/evaluations/{id}     # Xóa đánh giá
POST   /api/v3/evaluations/batch    # Lưu hàng loạt

# Sync
GET    /api/v3/sync/pull            # Kéo dữ liệu mới
POST   /api/v3/sync/push            # Đẩy dữ liệu local
GET    /api/v3/sync/status          # Trạng thái đồng bộ

# Report
GET    /api/v3/reports              # Lấy danh sách báo cáo
POST   /api/v3/reports/generate     # Tạo báo cáo
GET    /api/v3/reports/{id}/export  # Xuất báo cáo (PDF/Excel)
```

---

## 🧪 KIỂM THỬ

### Chạy tests Laravel

```bash
cd laravel_backend
php artisan test
# hoặc
./vendor/bin/phpunit
```

### Chạy tests Flutter

```bash
cd flutter_app
flutter test
flutter test --coverage  # Báo cáo coverage
```

---

## 📦 BUILD & DEPLOY

### Build Laravel cho production

```bash
cd laravel_backend

# Cài đặt dependencies production
composer install --optimize-autoloader --no-dev

# Cache cấu hình
php artisan config:cache
php artisan route:cache
php artisan view:cache

# Chạy migration
php artisan migrate --force
```

### Build Flutter APK

```bash
cd flutter_app

# Build APK
flutter build apk --release

# Build App Bundle
flutter build appbundle --release

# File output:
# build/app/outputs/flutter-apk/app-release.apk
```

### Build Flutter IPA (iOS - chỉ trên Mac)

```bash
cd flutter_app

# Build iOS
flutter build ios --release

# Mở Xcode để archive
open ios/Runner.xcworkspace
```

---

## 🐳 CHẠY VỚI DOCKER

```bash
# Build và chạy
docker-compose up -d

# Dừng
docker-compose down

# Xem logs
docker-compose logs -f
```

**`docker-compose.yml`**

```yaml
version: '3.8'

services:
  mysql:
    image: mysql:8.0
    environment:
      MYSQL_DATABASE: security_system
      MYSQL_ROOT_PASSWORD: root
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql

  laravel:
    build: ./laravel_backend
    ports:
      - "8000:8000"
    depends_on:
      - mysql
    environment:
      DB_HOST: mysql
      DB_PASSWORD: root

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    ports:
      - "8080:80"
    environment:
      PMA_HOST: mysql

volumes:
  mysql_data:
```

---

## 📝 CÁC LỆNH LARAVEL ARTISAN

```bash
# Xóa cache
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear

# Tạo model
php artisan make:model ModelName -m

# Tạo controller
php artisan make:controller Api/v3/ControllerName

# Tạo seeder
php artisan make:seeder SeederName

# Tạo migration
php artisan make:migration create_table_name

# Chạy queue worker
php artisan queue:work

# Tạo báo cáo hàng ngày
php artisan report:daily

# Đồng bộ file chờ
php artisan sync:pending

# Gửi cảnh báo bảo mật
php artisan alerts:send

# Backup database
php artisan backup:run

# Quét mật khẩu
php artisan scan:passwords

# Quét web
php artisan scan:web
```

---

## 📝 CÁC LỆNH FLUTTER

```bash
# Cài đặt dependencies
flutter pub get

# Chạy ứng dụng
flutter run

# Chạy specific device
flutter run -d android
flutter run -d ios
flutter run -d chrome

# Build APK
flutter build apk --release

# Build App Bundle
flutter build appbundle --release

# Build iOS
flutter build ios --release

# Build Web
flutter build web --release

# Chạy tests
flutter test

# Phân tích code
flutter analyze

# Định dạng code
flutter format lib/

# Clean project
flutter clean
```

---

## 🔧 XỬ LÝ LỖI THƯỜNG GẶP

### Lỗi 1: Không kết nối được database

```bash
# Kiểm tra MySQL đang chạy
sudo systemctl status mysql

# Kiểm tra thông tin trong .env
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=security_system
DB_USERNAME=root
DB_PASSWORD=
```

### Lỗi 2: Flutter không tìm thấy thiết bị

```bash
# List các thiết bị
flutter devices

# Android: mở emulator
flutter emulators --launch <emulator_id>

# iOS: mở simulator (Mac only)
open -a Simulator
```

### Lỗi 3: API connection refused

```bash
# Kiểm tra Laravel server đang chạy
curl http://localhost:8000/api/v3/health

# Flutter Android emulator: dùng 10.0.2.2
# Flutter iOS simulator: dùng localhost
# Thiết bị thật: dùng IP máy tính (192.168.x.x)
```

### Lỗi 4: Migration lỗi

```bash
# Rollback và migrate lại
php artisan migrate:rollback
php artisan migrate:fresh --seed
```

---

## 👥 ĐÓNG GÓP

1. Fork dự án
2. Tạo branch mới: `git checkout -b feature/ten-tinh-nang`
3. Commit thay đổi: `git commit -m 'Add feature'`
4. Push lên branch: `git push origin feature/ten-tinh-nang`
5. Tạo Pull Request

---

## 📄 GIẤY PHÉP

Dự án được phân phối dưới giấy phép MIT.

---

## 📧 LIÊN HỆ

| Thông tin | Giá trị |
|-----------|---------|
| **Email** | support@security-system.com |
| **Website** | https://security-system.com |
| **GitHub** | https://github.com/security-system |

---

## ✅ CHECKLIST TRIỂN KHAI

- [ ] Cài đặt PHP 8.x và Composer
- [ ] Cài đặt MySQL và tạo database
- [ ] Cài đặt Flutter SDK
- [ ] Clone dự án
- [ ] Cài đặt dependencies Laravel
- [ ] Cấu hình file .env
- [ ] Chạy migration và seeder
- [ ] Chạy Laravel server
- [ ] Cài đặt dependencies Flutter
- [ ] Cấu hình API URL trong Flutter
- [ ] Chạy Flutter app
- [ ] Kiểm tra kết nối API
- [ ] Kiểm tra chức năng đăng nhập
- [ ] Kiểm tra đánh giá
- [ ] Kiểm tra đồng bộ offline

---

## 📌 GHI CHÚ

- **Môi trường development**: Dùng `php artisan serve` và `flutter run`
- **Môi trường production**: Dùng Nginx/Apache cho Laravel, build APK/IPA cho Flutter
- **Backup database**: Chạy `php artisan backup:run` định kỳ
- **Queue worker**: Luôn chạy `php artisan queue:work` trong production

---

**© 2025 Security Evaluation System. All rights reserved.**
```

---

## 📁 CÁC FILE README PHỤ

### `docs/API_DOCS.md`

```markdown
# API DOCUMENTATION

## Base URL
- Development: `http://localhost:8000/api/v3`
- Production: `https://api.security-system.com/api/v3`

## Authentication
All API requests require Bearer token:
```
Authorization: Bearer {your_token}
```

## Endpoints

### Auth
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/auth/login` | Đăng nhập |
| POST | `/auth/logout` | Đăng xuất |
| POST | `/auth/refresh` | Refresh token |
| POST | `/auth/verify-otp` | Xác thực OTP |

### User
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/user/profile` | Lấy thông tin user |
| PUT | `/user/profile` | Cập nhật profile |

### Evaluation
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/evaluations` | Lấy danh sách |
| POST | `/evaluations` | Tạo mới |
| PUT | `/evaluations/{id}` | Cập nhật |
| DELETE | `/evaluations/{id}` | Xóa |
```

### `docs/DEPLOYMENT.md`

```markdown
# DEPLOYMENT GUIDE

## Production Deployment

### Laravel
1. Set environment variables
2. Run migrations
3. Configure web server (Nginx/Apache)
4. Setup queue worker
5. Configure cron jobs

### Flutter
1. Build APK for Android
2. Build IPA for iOS
3. Publish to App Store/Google Play

## Server Requirements
- PHP 8.1+
- MySQL 8.0+
- Nginx/Apache
- Redis (optional)
```

---

## ✅ TỔNG KẾT

| File | Vị trí | Mục đích |
|------|--------|----------|
| `README.md` | Gốc dự án | Tổng quan, cài đặt, chạy |
| `API_DOCS.md` | `docs/` | Tài liệu API |
| `DEPLOYMENT.md` | `docs/` | Hướng dẫn triển khai |
| `USER_GUIDE.md` | `docs/` | Hướng dẫn sử dụng |

