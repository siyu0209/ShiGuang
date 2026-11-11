<div align="center">

<img src="docs/logo.svg" width="112" alt="ShiGuang logo">

# 拾光 · ShiGuang

**抖音 / B站 无水印视频下载 · Android 客户端**

[![Release](https://img.shields.io/github/v/release/siyu0209/ShiGuang?include_prereleases&style=flat-square)](https://github.com/siyu0209/ShiGuang/releases)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Android%208.0%2B%20(arm64--v8a)-3DDC84?style=flat-square&logo=android&logoColor=white)](#-安装)
[![Kotlin](https://img.shields.io/badge/Kotlin-Jetpack%20Compose-7F52FF?style=flat-square&logo=kotlin&logoColor=white)](#-技术架构)

[下载](#-下载) · [功能](#-功能特性) · [安装](#-安装) · [技术架构](#-技术架构) · [English](#english)

</div>

---

## 📥 下载

| 文件 | 版本 | 大小 | 直链 |
| --- | --- | --- | --- |
| `ShiGuang-1.0.0-debug.apk` | 1.0.0 (versionCode 1) | 67.1 MB | [仓库下载](https://github.com/siyu0209/ShiGuang/raw/main/ShiGuang-1.0.0-debug.apk) · [Releases](https://github.com/siyu0209/ShiGuang/releases) |

校验信息：

```
SHA-256   c6cc4851082136eeb1abd43bb1e3b0dd6ec780a831ef1755d3580240637fa2e5
大小       70,329,648 字节
签名证书   1367f55ddabae46ed93a1b4709b9133e6016056a76575e9ca04d5617129eb70e  (APK Signature Scheme v2)
```

> 当前发行包为 `debug` 构建（`application-debuggable=true`，包名 `com.shiguang.downloader.debug`），可与正式版共存安装。首次安装需在系统设置中允许「安装未知来源应用」。

---

## ✨ 功能特性

- **无水印解析** —— 从分享链接中提取原始播放地址，输出干净的视频文件。
- **抖音链接直达** —— 注册 `www.douyin.com` / `v.douyin.com` / `www.iesdouyin.com` 的 `VIEW` 意图过滤器，在浏览器或抖音里点「分享 → 打开方式 → 拾光」即可唤起。
- **系统分享接收** —— 支持 `text/plain` 的 `SEND` 意图，长按复制链接后从任意应用分享过来即可。
- **前台服务下载** —— 下载任务运行在 `DownloadService` 前台服务中，通知栏实时显示进度，切后台、锁屏不中断。
- **音视频合流** —— 内置 FFmpeg / FFprobe，分离的音轨与视频轨在本地合并成可直接播放的 MP4。
- **Python 解析内核** —— 通过 Chaquopy 嵌入 CPython 运行时并随包分发 `yt-dlp`，解析规则可随上游更新，不依赖自建服务端。
- **本地处理** —— 解析与合流全部在设备上完成，无需登录账号。

---

## 📲 安装

**环境要求**

| 项目 | 要求 |
| --- | --- |
| 系统版本 | Android 8.0 (API 26) 及以上 |
| 目标 SDK | 35 (Android 15) |
| CPU 架构 | `arm64-v8a`（64 位 ARM，绝大多数在售机型） |
| 存储 | 约 150 MB 可用空间（安装包 + 运行时解压） |

**步骤**

1. 下载 `ShiGuang-1.0.0-debug.apk`。
2. 在文件管理器中点击安装；若被拦截，按提示开启「允许来自此来源的应用」。
3. 首次启动授予「通知」权限（用于下载进度通知）。
4. 复制抖音 / B站 分享链接 → 打开拾光 → 粘贴解析 → 选择清晰度 → 下载。

> Android 7.0 及更早版本、以及 32 位（`armeabi-v7a`）设备无法安装，因为发行包只包含 `arm64-v8a` 原生库。

---

## 🧱 技术架构

| 层次 | 组件 |
| --- | --- |
| 语言 / UI | Kotlin，Jetpack Compose（Material 3），Navigation + ViewModel |
| 网络 | OkHttp、Jackson（JSON 解析） |
| 媒体 | Media3 / ExoPlayer（预览），FFmpeg + FFprobe（合流、转码） |
| 解析内核 | Chaquopy 嵌入 CPython，内置 `yt-dlp`（`res/raw/ytdlp`），QuickJS 执行站点 JS |
| 后台 | `DownloadService`（前台服务 + `FOREGROUND_SERVICE_DATA_SYNC`）、协程 |
| 构建 | AGP 8.7.3，compileSdk 35，minSdk 26，仅 `arm64-v8a` |

**包内原生库**

| 文件 | 大小 | 用途 |
| --- | --- | --- |
| `lib/arm64-v8a/libffmpeg.zip.so` | 34.0 MB | FFmpeg 主库（压缩存放，运行时解压） |
| `lib/arm64-v8a/libpython.zip.so` | 13.6 MB | CPython 标准库 |
| `lib/arm64-v8a/libqjs.so` | 0.9 MB | QuickJS 引擎 |
| `lib/arm64-v8a/libffmpeg.so` / `libffprobe.so` | 0.3 MB / 0.2 MB | 加载器 |

**权限说明**

| 权限 | 用途 |
| --- | --- |
| `INTERNET` / `ACCESS_NETWORK_STATE` | 解析、下载视频 |
| `POST_NOTIFICATIONS` | 显示下载进度通知 |
| `FOREGROUND_SERVICE` / `FOREGROUND_SERVICE_DATA_SYNC` | 后台持续下载 |
| `READ_EXTERNAL_STORAGE` (≤ API 32) / `WRITE_EXTERNAL_STORAGE` (≤ API 28) | 保存文件到公共目录 |

---

## 📦 仓库内容

```
ShiGuang/
├─ ShiGuang-1.0.0-debug.apk   发行包
├─ README.md                  本文件
├─ CHANGELOG.md               版本记录
├─ THIRD_PARTY_NOTICES.md     第三方组件与许可
├─ LICENSE                    MIT
└─ docs/
   └─ logo.svg                应用标识
```

本仓库是《拾光》的公开主页与发行渠道，提供可直接安装的构建产物、版本记录与组件清单。

---

## ⚠️ 使用须知

- 请仅下载你**有权保存**的内容，例如自己发布的视频、已获授权的素材，或平台允许离线缓存的公开内容。
- 二次分发他人作品前，请取得著作权人许可并遵守平台服务条款。
- 本项目与抖音、哔哩哔哩及其关联公司无任何隶属或合作关系，相关商标归各自权利人所有。

---

## 🤝 参与贡献

欢迎通过 [Issues](https://github.com/siyu0209/ShiGuang/issues) 反馈解析失效、机型兼容等问题，提交时请附上：

1. 分享链接（可脱敏，保留 `https://v.douyin.com/xxxxxx/` 形态即可）
2. 应用版本与 Android 版本
3. `adb logcat` 中 `com.shiguang.downloader` 相关日志

---

## 📄 许可证

本项目代码与文档以 [MIT License](LICENSE) 发布。随包分发的第三方组件（FFmpeg、yt-dlp、CPython、QuickJS 等）遵循其各自许可，详见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

---

## English

**ShiGuang (拾光)** is an Android client that downloads watermark-free videos from Douyin (TikTok China) and Bilibili.

- **Download:** [`ShiGuang-1.0.0-debug.apk`](https://github.com/siyu0209/ShiGuang/raw/main/ShiGuang-1.0.0-debug.apk) (67.1 MB)
- **Requirements:** Android 8.0+ (API 26), `arm64-v8a` only
- **How it works:** share a Douyin/Bilibili link to the app (or open it directly), and a foreground service resolves the original media URL with the bundled `yt-dlp` + Python runtime, then muxes audio and video locally with FFmpeg.
- **Build facts:** Kotlin + Jetpack Compose, `compileSdk 35`, `minSdk 26`, package `com.shiguang.downloader.debug`, `versionName 1.0.0-debug`. This is a debuggable build.

```
SHA-256  c6cc4851082136eeb1abd43bb1e3b0dd6ec780a831ef1755d3580240637fa2e5
```

Please only download content you are entitled to keep. Not affiliated with Douyin or Bilibili.

Licensed under the [MIT License](LICENSE). Third-party components keep their own terms — see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
