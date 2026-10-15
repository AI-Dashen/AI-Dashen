# AI 大神 (AI-Dashen) ｜ 端侧工程 · 跨设备协同 · 本地工作流

> 专注解决真实工程痛点：把安卓手机现有输入法变成 Windows 的加密语音输入终端（VoiceInput2PC）；在 Android/Termux ARM64 环境推进大体积 APK 索引与按需反编译分析（rea 分支增强）；构建基于 yt-dlp 与 whisper.cpp 的 Windows 本地视频转写与故事卡生成流水线（douyin-story-pipeline）。

## 正在解决的三个问题

| 项目 | 你能获得什么 | 技术落点 |
| --- | --- | --- |
| [rea](https://github.com/AI-Dashen/rea) | 将大体积 APK 索引、按需反编译与受控 Frida 挂载带入 Android/Termux ARM64 环境。 | Android/Termux ARM64 本地适配与大体积 APK SQLite 索引及按需反编译 |
| [VoiceInput2PC](https://github.com/AI-Dashen/VoiceInput2PC) | 不买麦克风、不传音频流，直接用口袋里的手机输入法向电脑光标位置安全口述文字。 | 应用层 HTTPS + 专用令牌 + 证书指纹固定，内置 Tailcat/WireGuard 跨网络加密通道 |
| [douyin-story-pipeline](https://github.com/AI-Dashen/douyin-story-pipeline) | 输入公开视频链接，在 Windows 本机自动完成限速下载、whisper.cpp 离线转写与结构化故事卡生成。 | 整合 yt-dlp + FFmpeg + whisper.cpp + Silero VAD，转写与卡片生成全流程在 Windows 本地完成 |

## 工程方式

- 克制务实：优先复用手头已有设备与成熟开源组件，用清晰的工程链路解决实际痛点
- 边界清晰：区分本地执行、网络传输与上游能力，严守权限最小化与数据安全边界
- 证据驱动：重视可复现构建、真实环境验证与结构化记录，不夸大未完成的远期特性

## 了解项目

每个仓库的 README 提供用途、技术特点和已知边界。安装包以对应 Releases 为准；工程原型、候选包与真机验证分别记录。

开源组件按其原始许可证使用，项目中的派生代码保留来源。
