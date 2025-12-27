# 编译指南

本指南按子项目列出了在本地编译 Simple Live 的步骤。建议使用与仓库保持一致的 Flutter 版本 `3.38.x`，并确保各平台的原生构建依赖（如 Android SDK、Xcode、桌面工具链）已经正确安装。

## 通用准备

1. 安装并配置 Flutter（包含 Dart SDK）。
2. 确认 `flutter --version` 正常输出且满足版本要求。
3. 拉取依赖：进入对应子项目后执行 `flutter pub get`（纯 Dart 包可用 `dart pub get`）。

## simple_live_core（核心库）

核心库本身无需单独编译成可执行文件，但在发布或运行示例前需要获取依赖：

```bash
cd simple_live_core
dart pub get
# 运行内置示例
dart run example/main.dart
```

## simple_live_console（控制台程序）

使用 Dart 原生编译为独立可执行文件：

```bash
cd simple_live_console
dart pub get
dart compile exe bin/simple_live_console.dart -o build/simple_live_console
```

编译完成后，`build/simple_live_console`（或在 Windows 上为 `.exe`）即可直接运行。例如：

```bash
./build/simple_live_console -i https://www.huya.com/123456
```

## simple_live_app（移动/桌面 Flutter 客户端）

常用的打包命令：

```bash
cd simple_live_app
flutter pub get

# Android 发布包（需已配置 Android SDK）
flutter build apk --release

# iOS 发布包（仅限 macOS，需已配置 Xcode）
flutter build ios --release

# 桌面版本（需在目标平台启用桌面支持）
flutter config --enable-windows-desktop
flutter config --enable-macos-desktop
flutter config --enable-linux-desktop
flutter build windows   # 或 macos/linux
```

生成的安装包位于 `build/` 目录下，对应各平台的默认输出位置。

## simple_live_tv_app（Android TV 客户端）

按照标准 Flutter Android 打包流程生成 APK：

```bash
cd simple_live_tv_app
flutter pub get
flutter build apk --release
```

如果需要自定义构建目标（如不同入口文件或风味），可在命令中追加 `--target` 或 `--flavor` 参数。
