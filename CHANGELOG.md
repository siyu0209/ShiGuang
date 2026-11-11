# 更新日志 · Changelog

本项目版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## [1.0.0] - 2026-11-11

首个公开版本。

### 新增

- 抖音分享链接解析与无水印下载，支持 `www.douyin.com`、`v.douyin.com`、`www.iesdouyin.com` 链接直接唤起。
- 系统分享接收（`text/plain`），可从任意应用把链接分享到拾光。
- `DownloadService` 前台服务下载队列，通知栏实时进度，后台不中断。
- FFmpeg / FFprobe 本地音视频合流，输出可直接播放的 MP4。
- 基于 Chaquopy 的 Python 解析内核，内置 `yt-dlp`，解析规则可随上游更新。
- Jetpack Compose (Material 3) 界面，支持深色模式。

### 已知问题

- 仅提供 `arm64-v8a` 原生库，32 位设备与模拟器（x86_64）无法安装。
- 当前为 `debug` 构建，`application-debuggable=true`，包名带 `.debug` 后缀，可与正式版共存。
- 解析依赖第三方平台接口，平台改版后可能出现临时失效，需等待 `yt-dlp` 上游更新。

### 构建信息

| 项目 | 值 |
| --- | --- |
| versionName | `1.0.0-debug` |
| versionCode | `1` |
| package | `com.shiguang.downloader.debug` |
| compileSdk | 35 |
| minSdk | 26 |
| targetSdk | 35 |
| ABI | `arm64-v8a` |
| AGP | 8.7.3 |
| APK SHA-256 | `c6cc4851082136eeb1abd43bb1e3b0dd6ec780a831ef1755d3580240637fa2e5` |
