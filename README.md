<div align="center">

<img src="assets/images/icon.png" alt="FlClash" width="88">

# FlClash Fork

基于 ClashMeta 的多平台代理客户端，保留旧版界面，去掉遥测与首次进入弹窗。

[![Release](https://img.shields.io/github/v/release/LangYa466/FlClash-fork?style=flat-square&label=release)](https://github.com/LangYa466/FlClash-fork/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/LangYa466/FlClash-fork/total?style=flat-square&logo=github)](https://github.com/LangYa466/FlClash-fork/releases)
[![License](https://img.shields.io/github/license/LangYa466/FlClash-fork?style=flat-square)](LICENSE)
[![Telegram](https://img.shields.io/badge/Telegram-channel-26A5E4?style=flat-square&logo=telegram&logoColor=white)](https://t.me/langya_channel)

[下载](#下载) · [与原版的区别](#与原版的区别) · [更新日志](CHANGELOG.md) · [从源码构建](#从源码构建)

</div>

## 与原版的区别

本项目 fork 自 [chen08209/FlClash](https://github.com/chen08209/FlClash)，代码基线是上游 **v0.8.99**（提交 `68c71b8`）。
上游在 0.9.x 重做了界面并改动了内核与存储，本 fork 不跟进这些改动，并额外删除了一批功能。下面是完整清单。

### 回退到 v0.8.99 后，没有的上游 0.9.x 内容

界面：

- iOS 风格的分层填充、字号体系与 Liquid Glass，以及 iOS 风格的开关、搜索栏、栏按钮和菜单
- 围绕"当前出口"重做的仪表盘，以及仪表盘布局编辑页
- 代理组卡片与代理组标签 chip
- 连接、请求、DNS 的表格视图
- 重新设计的主题色与 iOS 风格取色器，深色模式对比度调整
- 可堆叠的底部弹层、上下文菜单、滑动选择弹出菜单
- 页面延伸到 Android 导航栏下方
- 桌面端侧边栏的系统材质模糊
- 底部的访问控制状态栏
- 托盘图标按状态着色

功能：

- 自定义配置编辑器，以及配置的导入与组装
- DNS、NTP、sniffer、TUN 的逐项设置，以及"通用覆写可选"
- 配置二维码与"手机到电视"的链接
- 配置详情里的外部资源管理
- 从代理菜单把节点加入本地代理
- 手动或在网络变化时清除 DNS 缓存
- Android 启动器快捷方式与一步式按需接入
- 法语、西班牙语、韩语界面（本 fork 只有简体中文、英语、日语、俄语）

底层：

- 用 gomobile 绑定的 Android 内核、Android 内核调用与事件移出主线程
- 自定义配置及其设置的数据库存储
- 超大配置不再崩溃的修复，Windows / Linux 系统代理、托盘和 Helper 的修复，以及 mihomo v1.19.33 更新
- 其它 v0.8.99 之后的修复

### 本 fork 另外删除的内容

- **IP 类型与质量**：删除"机房 / 住宅 / 移动 / 商业"类型标签、"质量 优 / 普通 / 风险"等级、多来源查询、详情面板和 3 天缓存。
  出口 IP 只显示为文本，也不能再点开详情。
- **免责声明**：删除首次进入时必须同意的免责声明页面，以及设置里的免责声明入口。
- **数据收集提示**：删除 Android 首次启动的"数据收集"弹窗。
- **崩溃上报**：删除设置里的"崩溃报告"开关。
- **Firebase**：Android 构建中删除 Firebase Crashlytics 与 Analytics 的依赖、Gradle 插件、符号上传任务、
  `google-services.json` 和 CI 里写入它的步骤，原生与 Dart 两侧的崩溃探测代码也一并删除。
- **相关测试**：删除只针对上述功能的测试文件，其余测试同步改掉了对应的断言。
- **第三方发布渠道**：删除 CI 里推送到 Telegram、Homebrew tap 和 F-Droid 仓库的步骤，以及 `release_telegram.py`
  和 Homebrew cask 模板。README 中的 F-Droid、Homebrew 安装方式和官网链接一并删除。

### 本 fork 另外修改的内容

- **更新检测**：改为读取 [LangYa466/FlClash-fork](https://github.com/LangYa466/FlClash-fork) 的最新 Release，
  tag 形如 `v0.9.3`，版本号高于当前版本才会提示更新。
- **链接**：关于页、Issue 模板、Release 模板、徽章和构建脚本中的仓库地址改为本仓库，Telegram 频道改为
  [t.me/langya_channel](https://t.me/langya_channel)。
- **CI 发布**：打 `v*` 标签后，只在本仓库构建并发布 GitHub Release 与 `SHA256SUMS`。

### 保留的部分

- WebDAV 备份与恢复保留，它只会连接你自己配置的服务器。
- 配置模型里的 `crashlytics`、`crashlyticsTip`、`disclaimerAccepted` 字段仍在，只是不再有任何界面或逻辑使用它们。
- 关于页里的 Clash.Meta 内核链接仍指向原作者的内核仓库，依赖与子模块地址也保持原样。

## 功能

- **一个应用覆盖 Android、Windows、macOS 和 Linux**，桌面端同时提供 x64 与 ARM64 版本。
- **mihomo（Clash.Meta）内核**：规则分流、代理组、延迟测试、系统代理与 TUN 模式。
- **配置管理**：通过订阅链接或文件导入配置，内置编辑器，支持覆写脚本以及自定义规则、代理和代理组。
- **实时查看**连接、请求、DNS 查询和日志。
- **Material You 设计**：支持动态取色、浅色与深色主题，布局随屏幕从手机到桌面自适应。
- **备份与恢复**：通过 WebDAV 或本地文件。
- **平台细节**：Android 上有快捷设置磁贴、分应用代理和 Android TV 支持；桌面端有托盘菜单和全局快捷键。
- **开源无广告**，以 GPL-3.0 协议发布。

## 下载

从 [GitHub Releases](https://github.com/LangYa466/FlClash-fork/releases/latest) 获取最新版本。

| 平台 | 安装包 | 说明 |
| --- | --- | --- |
| Android | `arm64-v8a`、`armeabi-v7a`、`x86_64` 三种 APK | 绝大多数手机选 `arm64-v8a`。 |
| Windows 10 及以上 | 安装版（`.exe`）或便携版（`.zip`），分 x64 与 ARM64 | 骁龙等 ARM 架构笔记本选 ARM64。 |
| macOS 12 及以上 | Apple Silicon 与 Intel 两种 DMG | |
| Linux | `.deb`、`.rpm` 和 AppImage，分 x64 与 ARM64 | 托盘依赖见下方说明。 |

**Linux 托盘图标**

`.deb` 安装包会自动安装所需依赖。使用 AppImage 或 `.rpm` 时，需要先安装 AyatanaAppIndicator 库，托盘图标才能显示：

```bash
sudo apt-get install libayatana-appindicator3-1   # Debian 与 Ubuntu
sudo dnf install libayatana-appindicator-gtk3     # Fedora
```

## 使用

**通过链接导入配置。** 打开下面格式的链接，即可把订阅导入 FlClash。`clashmeta://` 和 `flclash://` 开头的链接同样可用。

```text
clash://install-config?url=<经过 URL 编码的订阅链接>
```

**Android 自动化。** Tasker、MacroDroid 等应用可以用下面的 Action 启动 Activity，从而启动、停止或切换代理：

```text
com.follow.clash.action.START
com.follow.clash.action.STOP
com.follow.clash.action.TOGGLE
```

在电脑上也可以通过 adb 触发：

```bash
adb shell am start -a com.follow.clash.action.TOGGLE
```

## 从源码构建

需要 [Flutter](https://docs.flutter.dev/get-started/install) 3.47（CI 使用 3.47.4）、[Go](https://go.dev/dl/) 1.26，
以及通过 rustup 安装的 [Rust](https://rustup.rs/)。桌面端需要在对应系统上构建，Android 在任意系统上都能构建。

```bash
git clone --recursive https://github.com/LangYa466/FlClash-fork.git
cd FlClash-fork
flutter pub get
dart setup.dart android   # 或 windows、macos、linux
```

安装包输出到 `dist/`。Go 内核和 Rust 库会在 Flutter 构建过程中一并编译。

| 平台 | 额外依赖 |
| --- | --- |
| Android | 带 NDK 的 Android SDK。加上 `--arch arm64` 可以只构建单个 ABI。 |
| Windows | 编译内核用的 GCC（MinGW-w64），以及打包安装程序用的 [Inno Setup](https://jrsoftware.org/isinfo.php) 6。 |
| macOS | Xcode 与 Node.js。脚本会通过 npm 安装 `appdmg`。 |
| Linux | Debian 或 Ubuntu。脚本会用 apt 安装构建所需的软件包，并下载 `appimagetool`。 |

其余选项可以运行 `dart setup.dart --help` 查看，例如用 `--targets` 只构建部分安装包格式。

## 支持

给仓库点一个 Star 是支持项目最简单的方式。问题讨论和更新通知请关注 [Telegram 频道](https://t.me/langya_channel)，
Bug 与功能建议请提交到 [GitHub Issues](https://github.com/LangYa466/FlClash-fork/issues)。

## 许可证

本项目以 [GPL-3.0 协议](LICENSE)发布，原始版权属于 [chen08209/FlClash](https://github.com/chen08209/FlClash)。
