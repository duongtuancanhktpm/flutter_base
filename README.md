# Flutter Base — Monorepo

Đây là một **monorepo** Flutter được quản lý bằng [Melos](https://melos.invertase.dev/) và [FVM](https://fvm.app/).

---

## 📁 Cấu trúc dự án

```
flutter_base/
├── apps/
│   ├── mobile/        # Ứng dụng Flutter Mobile
│   └── web/           # Ứng dụng Flutter Web
└── packages/
    └── ui_kit/        # Package UI dùng chung
```

---

## 🛠 Công cụ sử dụng

### [Melos](https://melos.invertase.dev/)
Melos là công cụ quản lý monorepo cho Dart/Flutter. Nó giúp:
- Liên kết (`bootstrap`) tất cả các packages trong workspace
- Chạy scripts đồng thời trên nhiều packages
- Quản lý phiên bản và publish packages

### [FVM (Flutter Version Management)](https://fvm.app/)
FVM giúp quản lý nhiều phiên bản Flutter trên cùng một máy, đảm bảo tất cả thành viên trong team sử dụng đúng phiên bản Flutter cho dự án.

---

## 🚀 Bắt đầu

### 1. Cài đặt FVM
```bash
dart pub global activate fvm
```

### 2. Cài đặt đúng phiên bản Flutter qua FVM
```bash
fvm install
```

### 3. (Tuỳ chọn) Alias lệnh `flutter` sang FVM — thêm vào shell profile của bạn

**PowerShell** (`$PROFILE`):
```powershell
function flutter { fvm flutter $args }
```

**Bash/Zsh** (`~/.bashrc` hoặc `~/.zshrc`):
```bash
alias flutter="fvm flutter"
```

### 4. Bootstrap toàn bộ workspace với Melos
```bash
dart run melos bs
```

Lệnh này sẽ chạy `flutter pub get` cho tất cả các packages và apps trong monorepo.

---

## 📦 Các packages & apps

| Tên | Đường dẫn | Mô tả |
|-----|-----------|-------|
| `mobile` | `apps/mobile` | Ứng dụng Flutter Mobile |
| `web` | `apps/web` | Ứng dụng Flutter Web |
| `ui_kit` | `packages/ui_kit` | Shared UI components |

---

## 🔧 Các lệnh Melos thường dùng

```bash
# Bootstrap — cài đặt dependencies cho toàn bộ workspace
dart run melos bs

# Chạy tất cả tests
dart run melos run test

# Kiểm tra lỗi (lint) toàn bộ workspace
dart run melos run lint
```
