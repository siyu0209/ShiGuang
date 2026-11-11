# 第三方组件与许可 · Third-Party Notices

《拾光》发行包内包含以下第三方组件。各组件的著作权与许可归其原作者所有，本项目的 MIT 许可不适用于它们。

## 运行时分发的二进制 / 资源

| 组件 | 包内位置 | 许可 | 项目主页 |
| --- | --- | --- | --- |
| **FFmpeg** (ffmpeg-kit 构建) | `lib/arm64-v8a/libffmpeg.zip.so`、`libffmpeg.so`、`libffprobe.so` | LGPL-2.1-or-later；若为 GPL 变体构建则为 GPL-2.0-or-later | https://ffmpeg.org · https://github.com/arthenica/ffmpeg-kit |
| **yt-dlp** | `res/raw/ytdlp` | Unlicense | https://github.com/yt-dlp/yt-dlp |
| **CPython** | `lib/arm64-v8a/libpython.zip.so`、`libpython.so` | PSF License 2.0 | https://www.python.org |
| **Chaquopy** | 构建期集成，Python 运行时加载 | MIT（运行时）；构建插件为商业授权 | https://chaquo.com/chaquopy/ |
| **QuickJS** | `lib/arm64-v8a/libqjs.so` | MIT | https://bellard.org/quickjs/ |

> FFmpeg 的构建变体（LGPL 或 GPL）取决于 ffmpeg-kit 的打包配置。若需重新分发本 APK 或其中的 FFmpeg 二进制，请以对应构建的许可条款为准，并保留上游版权声明。

## 主要开源依赖（Android 侧）

以下库以 AAR / 源码形式编译进 `classes*.dex`，均按其原始许可分发：

| 组件 | 许可 |
| --- | --- |
| AndroidX（`core-ktx`、`activity-compose`、`lifecycle-*`、`navigation-*`、`media3`、`exoplayer`、`profileinstaller`、`startup` 等） | Apache-2.0 |
| Jetpack Compose（`runtime`、`ui`、`foundation`、`material`、`material3`、`animation`、`tooling`） | Apache-2.0 |
| Kotlin Standard Library / `kotlinx.coroutines` | Apache-2.0 |
| OkHttp / Okio | Apache-2.0 |
| Jackson（`core`、`databind`、`annotations`） | Apache-2.0 |
| ExoPlayer 图标资源 | Apache-2.0 |

## 商标

「抖音」「Douyin」为北京字节跳动科技有限公司的商标；「哔哩哔哩」「Bilibili」为上海幻电信息科技有限公司的商标。本项目与上述公司无隶属、赞助或合作关系，仅在功能上兼容其公开的分享链接格式。
