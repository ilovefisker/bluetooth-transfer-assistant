# 蓝牙文字与文件传输助手

Android → Windows 本地蓝牙传输工具。文字接收后自动在记事本显示，文件通过手机系统蓝牙分享传输。

## 下载与安装

- [完整源码 ZIP](bluetooth-transfer-assistant-mit-source.zip)：包含 Android、Windows、BLE 桥接器固件、协议测试及构建脚本。解压后进入 github-release-source 文件夹。
- [手机与电脑安装使用说明](INSTALL.md)：分别说明 APK、Windows EXE 与源码编译的使用方式。

当前以源码压缩包形式发布，代码尚未在仓库网页中按目录展开；下载 ZIP 后可查看完整目录与源码。当前没有上传 APK 或预编译 EXE。

## 功能

- 安卓“文字传输 / 文件传输”双标签页，辅助设置折叠。
- 文字采用 RMW 协议，经经典蓝牙 SPP 或配套 BLE 串口桥发送，校验完整性并回复 ACK。
- Windows 接收器优先选择 COM3，接收文字后自动打开记事本。
- 可选监测指定目录：新建或更新文件写入稳定约 6 秒后打开保存目录。
- 不含 AI、医学知识库或内置 OCR；OCR 结果可从其他应用复制后粘贴。

## 系统与构建

| 平台 | 版本与入口 |
| --- | --- |
| Android 6.0+ | 0.3.1 Java 源码；android/build.sh，需 JDK 17、SDK Platform 35、Build Tools 35.0.0 |
| Win7 32 位 | windows/BUILD-AND-RUN-WIN7-X86.bat |
| Win11 Intel/AMD 64 位 | windows/BUILD-AND-RUN-WIN11-X64.bat，非 ARM64 版本 |

Windows 构建需要兼容的 .NET Framework 4.x 和 csc.exe，不要求安装 Visual Studio。成功后在对应 bin 子目录生成 EXE。

Android 首次构建生成本地测试密钥。仓库不提供私钥；不同构建者的 APK 签名不同，不能保证相互覆盖安装。公开源码没有预填个人蓝牙地址。

## 两种通道

文字模式需要电脑 SPP 传入 COM 与配套接收器；文件模式需要 Windows 系统蓝牙“接收文件”，手机仍需在分享面板手动选择蓝牙和设备。能发文件不代表一定支持 SPP。

目录监测只观察指定目录顶层的文件变化，不是精确蓝牙完成通知；其他软件写入也可能触发。请使用专用接收目录。

## 验证与安全

五项 Node 协议测试已通过，用户曾测试部分传输功能；Windows 两种架构、新版界面和蓝牙驱动兼容性尚未完成系统性验证。不将构建成功视为全平台兼容保证。

APK 不声明互联网权限，但系统分享面板的其他应用可能联网，请不要误选网盘或聊天应用。SHA-256 仅校验完整性，不提供应用层加密或身份认证。请核对设备，先用脱敏内容测试，并遵守所在单位内网设备接入规定。

记事本回退文件保存在 `%TEMP%\RemoteMedWriter`，不自动删除。接收器不会自动执行收到的文件。

## 许可证与素材

采用 [MIT License](LICENSE)。图标由项目所有者确认系 AI 生成，来源及使用说明见 [ASSETS.md](ASSETS.md)。不对特定用途适用性或素材不侵权作保证。

## 反馈

请提供手机型号、Android/Windows 版本、Windows 位数、传输模式和脱敏错误截图。不要上传患者资料、密钥或个人设备地址。
