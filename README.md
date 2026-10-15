# AI 大神 (AI-Dashen) ｜ 端侧工程 · 跨设备协同 · 本地工作流

> 专注解决真实工程痛点：把安卓手机现有输入法变成 Windows 的加密语音输入终端（VoiceInput2PC）；在 Android/Termux ARM64 环境推进大体积 APK 索引与按需反编译分析（rea 分支增强）；构建基于 yt-dlp 与 whisper.cpp 的 Windows 本地视频转写与故事卡生成流水线（douyin-story-pipeline）。

## 把真实设备，接成能工作的工具链

### [Android/Termux 逆向分析工作台增强版 · rea](https://github.com/AI-Dashen/rea)

将大体积 APK 索引、按需反编译与受控 Frida 挂载带入 Android/Termux ARM64 环境。

[![工作流架构示意](https://raw.githubusercontent.com/AI-Dashen/rea/main/docs/assets/project-workflow.png)](https://github.com/AI-Dashen/rea)

- **多DEX mmap映射与SQLite符号索引**：减少一次性反编译整个 APK 的资源压力，结构索引可持久化并供后续查询使用；首次建库仍有读取和解析成本，未公布统一检索延迟指标。
- **DEX 索引与 JADX 单类反编译**：先定位目标类，再生成相关 Java 代码；Ghidra 处理 Native 路径，两类引擎各司其职，不把 SO 当 Java 类反编译。
- **Evidence Graph v2图谱数据模型**：为证据保留来源、精度、置信度和稳定指纹，便于区分观察事实与推断；并不代表所有动态数据已自动接入。

[查看实现、使用示例与验证范围 →](https://github.com/AI-Dashen/rea)

### [手机语音输入电脑 · VoiceInput2PC](https://github.com/AI-Dashen/VoiceInput2PC)

不买麦克风、不传音频流，直接用口袋里的手机输入法向电脑光标位置安全口述文字。

[![工作流架构示意](https://raw.githubusercontent.com/AI-Dashen/VoiceInput2PC/main/docs/assets/project-workflow.png)](https://github.com/AI-Dashen/VoiceInput2PC)

- **外置ASR与增量文本Diff提取**：本应用无需申请麦克风权限，也不必部署 ASR 模型；识别算力与联网行为由用户选用的手机输入法承担。已发送前缀被改写时暂停核对，避免误删电脑文本。
- **Win32 Unicode键盘注入与窗口句柄绑定**：通过 Unicode 键盘输入减少对剪贴板的占用；输入绑定目标窗口，窗口变化时暂停，降低输错位置的风险。
- **内置 Tailcat 跨网络数据通道**：在局域网不可直连时提供 WireGuard / DERP 路径；公司网络、防火墙和配对凭据生命周期仍影响连接，不承诺任意网络免配置可用。

[查看实现、使用示例与验证范围 →](https://github.com/AI-Dashen/VoiceInput2PC)

### [影记 ClipScribe：本地短视频转写与故事卡流水线 · douyin-story-pipeline](https://github.com/AI-Dashen/douyin-story-pipeline)

输入公开视频链接，在 Windows 本机自动完成限速下载、whisper.cpp 离线转写与结构化故事卡生成。

[![工作流架构示意](https://raw.githubusercontent.com/AI-Dashen/douyin-story-pipeline/main/docs/assets/project-workflow.png)](https://github.com/AI-Dashen/douyin-story-pipeline)

- **批次限制、随机请求间隔与下载归档**：单轮有数量上限并在请求间等待，archive记录帮助去重；这是保守采集策略，不保证平台永不限制请求。
- **whisper.cpp (ggml量化模型) + Silero VAD纯本地转写**：本地模型和 VAD 承担转写，减少云端识别依赖；下载仍需网络，准确度和速度取决于音频、模型与电脑性能。
- **EXE薄壳启动器与PowerShell业务脚本分离架构**：既满足普通用户双击图形界面一键运行的需求，又避免单文件自解压EXE每次退出时丢失内置缓存，同时让开发者能直接审计和热修改底层`.ps1`处理逻辑。

[查看实现、使用示例与验证范围 →](https://github.com/AI-Dashen/douyin-story-pipeline)

## 工程方式

- 克制务实：优先复用手头已有设备与成熟开源组件，用清晰的工程链路解决实际痛点
- 边界清晰：区分本地执行、网络传输与上游能力，严守权限最小化与数据安全边界
- 证据驱动：重视可复现构建、真实环境验证与结构化记录，不夸大未完成的远期特性

图为架构与工作流示意，不是运行截图。各项目的实现、实验和未验证范围在对应仓库分别标记；上游代码与第三方引擎保留来源及许可证。
