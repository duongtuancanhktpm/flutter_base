# Flutter Base — Monorepo

A Flutter **monorepo** managed with [Melos](https://melos.invertase.dev/) and [FVM](https://fvm.app/).

---

## 📁 Project Structure

```
flutter_base/
├── apps/
│   ├── mobile/        # Flutter Mobile application
│   └── web/           # Flutter Web application
└── packages/
    └── ui_kit/        # Shared UI component library
```

---

## 🛠 Tools

### [Melos](https://melos.invertase.dev/)
Melos is a monorepo management tool for Dart/Flutter projects. It helps:
- Bootstrap all packages in the workspace with a single command
- Run scripts across multiple packages simultaneously
- Manage versioning and package publishing

### [FVM (Flutter Version Management)](https://fvm.app/)
FVM allows managing multiple Flutter versions on the same machine, ensuring all team members use the correct Flutter version for the project.

---

## 🚀 Getting Started

### 1. Install FVM
```bash
dart pub global activate fvm
```

### 2. Install the correct Flutter version via FVM
```bash
fvm install
```

### 3. (Optional) Alias the `flutter` command to FVM — add to your shell profile

**PowerShell** (`$PROFILE`):
```powershell
function flutter { fvm flutter $args }
```

**Bash/Zsh** (`~/.bashrc` or `~/.zshrc`):
```bash
alias flutter="fvm flutter"
```

### 4. Bootstrap the entire workspace with Melos
```bash
dart run melos bs
```

This runs `flutter pub get` for all packages and apps in the monorepo.

---

## 📦 Packages & Apps

| Name | Path | Description |
|------|------|-------------|
| `mobile` | `apps/mobile` | Flutter Mobile application |
| `web` | `apps/web` | Flutter Web application |
| `ui_kit` | `packages/ui_kit` | Shared UI components |

---

## 🔧 Common Melos Commands

```bash
# Bootstrap — install dependencies for the entire workspace
dart run melos bs

# Run all tests
dart run melos run test

# Run lint checks across the workspace
dart run melos run lint
```
