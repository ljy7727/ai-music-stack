# AI 音乐工具栈 · 项目总表（功能 / Star / 评分 / 能不能在小主机上跑）

一套本地部署的开源 AI 音乐工具组合（15 个项目的落地记录），覆盖
**人声分离 → 变声 → 歌声合成 → 编曲 → 整首歌生成 → 音效 → 视频配音效** 的完整链路。

> 整理日期：**2026-10-12**
> Star 数据：GitHub API 实时读取（当日快照）
> 评分：本表自评，0–10 分，三个维度加权 —— **效果 50% + 成熟度 30% + 易用性 20%**
> 「小主机」指 **Intel Core Ultra 5 125H**（Meteor Lake 笔记本，无独显）
>
> **配套文档**
> - [`docs/总说明.md`](docs/总说明.md) —— 15 个项目的分组说明、启动方式、网络与端口备注
> - [`docs/选型排查-2026-10-12.md`](docs/选型排查-2026-10-12.md) —— 为什么是这 15 个（GitHub 选型体检报告）

---

## 一、一句话结论

| 问题 | 答案 |
|---|---|
| 现在这套组合是不是最优选？ | **是。** 15 个项目覆盖了「分离 → 变声 → 歌声合成 → 编曲 → 整首歌生成 → 音效 → 视频配音效」完整链路，且每个环节选的都是当前开源最强或唯一可用方案。 |
| 最大的功能空白补上了吗？ | **补上了。** 原本缺「一句话出一整首歌」，现在由 **ACE-Step 1.5** 承担（13.4k★，MIT 可商用）。 |
| 人声分离装了吗？ | **装了两套。** 官方 GUI **UVR5 v5.6**（26.6k★）+ 脚本化的 **audio-separator**（1.4k★，已实测分离通过）。 |
| 那台 Ultra 5 125H 能跑吗？ | **一半能跑、一半勉强。** 详见第四节：分离类 ✅、变声 ✅、歌声合成 ⚠、大模型生成类 ⚠/❌。 |

---

## 二、总表（15 个项目）

按「本机是否已装好」排序。⭐=Star 数，「评分」为 10 分制。

| # | 项目 | 主要功能 | ⭐ Star | 许可 | 评分 | Ultra 5 125H |
|---|---|---|---|---|---|---|
| 1 | **UVR5**<br><sub>Anjok07/ultimatevocalremovergui</sub> | 人声/伴奏分离、多轨、去混响/去噪/去回声、内置 Matchering 母带匹配、对轨对齐、批量处理，**官方图形界面**（已装 **Roformer BETA 版**，四代模型全支持） | 26,571 | MIT | **9.0** | ✅ **能跑**（CPU 一首歌几分钟～十几分钟；官方另有 DirectML 版可用 Arc 核显） |
| 2 | **VocalSeparator**<br><sub>karaokenerds/python-audio-separator</sub> | 同一批 UVR 模型的**脚本/网页版**：人声·伴奏·四轨·六轨·卡拉OK·去混响·降噪 | 1,413 | MIT | **8.5** | ✅ **能跑**（CPU 慢；换机需重装 CPU 版 torch） |
| 3 | **ACE-Step 1.5**<br><sub>ace-step/ACE-Step-1.5</sub> | **歌词/文字 → 整首歌**（写词+编曲+演唱+混音）、翻唱、局部重绘、人声配伴奏、LoRA、50+ 语言 | 13,432 | MIT | **9.2** | ⚠️ **勉强**（≈9GB 权重；官方支持 Intel XPU 核显加速，纯 CPU 一首歌要很久） |
| 4 | **RVC**<br><sub>RVC-Project/…-Voice-Conversion-WebUI</sub> | **人声变声 / 翻唱**，可自训音色模型 | 38,693 | MIT | **9.0** | ✅ **能跑**（CPU 可接受；另有 DirectML 分支可走核显） |
| 5 | **SoulX-Singer**<br><sub>Soul-AILab/SoulX-Singer</sub> | **零样本歌声合成**（30 秒参考音色就唱新歌，F0/MIDI 双控，中/英/粤）+ 免转写翻唱(SVC) | 997 | Apache-2.0 | **8.0** | ⚠️ **勉强**（权重 5.35GB，CPU 一首歌十几～几十分钟） |
| 6 | **DiffSinger + OpenUtau**<br><sub>openvpi/DiffSinger</sub> | **音符级**歌声合成，手工调音高/音素，可控性最强 | 3,220 | Apache-2.0 | **8.5** | ✅ **能跑**（模型小，CPU 秒级～十几秒） |
| 7 | **MOSS-TTS / MOSS-SoundEffect**<br><sub>OpenMOSS/MOSS-TTS</sub> | 中英双语**语音合成** + **音效生成**（48 kHz，Apache-2.0 可商用） | 4,198 | Apache-2.0 | **8.0** | ⚠️ **勉强**（≈10GB 权重） |
| 8 | **Stable Audio 3**<br><sub>Stability-AI/stable-audio-3</sub> | 文生**音乐/音效**（medium / large 两档） | 798 | MIT | **8.0** | ⚠️ **勉强**（medium 权重 9.9GB；CPU 生成几十秒音频需数分钟起） |
| 9 | **Stable Audio Open**<br><sub>Stability-AI/stable-audio-tools</sub> | 文生**短音频/音效**（1.1B，轻量档） | 3,881 | MIT | **7.5** | ⚠️ **勉强**（CPU 可跑，慢） |
| 10 | **MMAudio**<br><sub>hkchengrex/MMAudio</sub> | **视频/文本 → 音效**（给视频自动配音效），也能文字生音效 | 2,278 | MIT | **8.0** | ❌ **不推荐**（需 ≈6GB 显存；核显共享内存勉强，CPU 极慢） |
| 11 | **MagentaRT 2**<br><sub>magenta/magenta-realtime</sub> | **实时**流式音乐生成（边弹边出音） | 1,821 | Apache-2.0 | **7.5** | ❌ **不能用**（官方只支持 Apple Silicon 与 NVIDIA GPU，无 CPU/核显推理路径） |
| 12 | **HeartMuLa / heartlib**<br><sub>HeartMuLa/heartlib</sub> | 歌词+标签 → 音乐（多语言）、HeartCodec 编解码、歌词转写、音频-文本对齐 | 3,746 | 见仓库 | **8.0** | ⚠️ **勉强**（3B 模型） |
| 13 | **YingMusic-Singer**<br><sub>GiantAILab/YingMusic-Singer</sub> | 零样本歌声合成 + **编辑**（无标注旋律引导） | 77 | 未声明 | **7.0** | ⚠️ **勉强**（同 SoulX 量级） |
| 14 | **TangoFlux**<br><sub>declare-lab/TangoFlux</sub> | 文生**音效**（轻量） | 885 | **非商用** | **7.0** | ✅ **能跑**（模型小，CPU 数分钟） |
| 15 | **Woosh**<br><sub>SonyResearch/woosh-sfx</sub> | 文生 / **视频→音效**（Sony AI） | 390 | Apache-2.0 | **7.0** | ⚠️ **勉强** |

> **图例**：✅ 能在 Ultra 5 125H 上正常用 ｜ ⚠️ 能跑但慢，只适合偶尔用/小片段 ｜ ❌ 实际不可用

---

## 三、按用途速查

| 你想做的事 | 用哪个 | 备选 |
|---|---|---|
| **把人声和伴奏拆开** | UVR5（图形界面） | VocalSeparator（脚本/网页） |
| **拆成鼓/贝斯/人声/其他四轨** | VocalSeparator（Demucs 四轨） | UVR5 |
| **卡拉OK 消主唱** | VocalSeparator（Mel-Roformer Karaoke 模型） | UVR5 |
| **去掉人声的混响/底噪** | VocalSeparator（De-Reverb / Denoise 模型） | UVR5 的 De-Echo 系列 |
| **让别人的声音变成我的音色（翻唱）** | RVC | SoulX-Singer 的 SVC 模式 |
| **给一段曲子配上真人声（唱歌）** | SoulX-Singer（零样本，给 30 秒参考） | YingMusic-Singer、DiffSinger |
| **我要一个音一个音精修唱腔** | DiffSinger + OpenUtau | — |
| **一句话生成一整首歌** | **ACE-Step 1.5** | HeartMuLa |
| **只要一段音乐/氛围音** | Stable Audio 3 / Open | MagentaRT |
| **生成音效（脚步、爆炸、雨声…）** | MOSS-SoundEffect / Stable Audio Open | TangoFlux、Woosh |
| **给视频自动配音效** | MMAudio | Woosh |
| **中文语音播报（配音）** | MOSS-TTS | — |

---

## 四、Intel Core Ultra 5 125H 专项分析

### 4.1 这颗芯片的底子

| 项目 | 规格 |
|---|---|
| CPU | 14 核 18 线程（4 性能核 + 8 能效核 + 2 低功耗核），最高 4.5 GHz |
| 核显 | **Intel Arc Graphics（7 个 Xe 核心，2.2 GHz）**，GPU INT8 算力 18 TOPS |
| NPU | Intel AI Boost，11 TOPS |
| 平台总算力 | **33 TOPS（INT8）** |
| 内存 | LPDDR5/X-7467 或 DDR5-5600，双通道，最高 96 GB（核显共享系统内存） |
| AI 框架 | OpenVINO™ / WindowsML / ONNX RT / DirectML / WebGPU |
| **独立显存** | **没有**（核显吃系统内存） |
| **CUDA** | **不支持** |

### 4.2 结论：为什么"一半能跑一半不能"

本目录里绝大多数项目的默认推理后端是 **NVIDIA CUDA**。这台机器没有 N 卡，所以只有三条路：

1. **退回 CPU 跑** —— 都能跑，但速度按模型大小断崖式下跌。
2. **走 Intel 官方加速栈**（DirectML / OpenVINO / PyTorch-XPU）—— 部分项目支持，需要换装对应的 torch / onnxruntime 版本。
3. **外部放一个 NVIDIA 显卡坞或换机** —— 本项目所有实测数据都出自 **RTX 4070 Ti SUPER 16GB**。

### 4.3 分档结论

| 档位 | 项目 | 说明 |
|---|---|---|
| **✅ 直接能用** | UVR5、VocalSeparator、RVC、DiffSinger、TangoFlux | 分离一首歌 CPU 上几分钟～十几分钟，可接受；RVC 变声一段几分钟；DiffSinger 秒级出结果 |
| **⚠️ 能跑但要等** | ACE-Step、SoulX-Singer、YingMusic-Singer、MOSS-TTS/SoundEffect、Stable Audio 3/Open、HeartMuLa、Woosh | 权重 3–10 GB，**建议至少 32 GB 内存**；单次生成从"几秒"变成"几十分钟"，适合偶尔用 |
| **❌ 不建议** | MMAudio、MagentaRT 2 | MMAudio 官方要求 ≈6 GB 显存且只在 Ubuntu 上测试过；MagentaRT 2 官方**只支持 Apple Silicon 和 NVIDIA GPU**，没有 CPU/Intel 核显的推理路径。这两项建议放到有 N 卡的机器上跑 |

### 4.4 想在小主机上提速，可以做什么

| 手段 | 适用项目 | 说明 |
|---|---|---|
| 装 **DirectML 版 UVR** | UVR5 | 官方 release 里有 `UVR_v5.6.0_setup_directml_old.exe`，可调用 Arc 核显 |
| 装 **PyTorch XPU 版**（`--index-url https://download.pytorch.org/whl/xpu`） | ACE-Step（自带 `requirements-xpu.txt`）、Stable Audio 3 | 让模型跑在 Arc 核显上，比纯 CPU 快数倍 |
| 用 **OpenVINO** 转模型 | ONNX 类模型（MDX-Net、VocalSeparator 的 onnx 模型） | Intel 官方加速栈，NPU 也能用上 |
| 用 **sherpa-onnx / faster-whisper** 之类 CPU 优化实现 | RVC、TangoFlux | 换推理后端，牺牲一点精度换速度 |
| **加内存到 32–64 GB** | 全部大模型 | 核显共享内存，内存越大能载入的模型越大 |

> 一句话：**这台机器当"轻量剪辑 + 分离 + 变声"用完全够；当"整首歌生成"用，需要耐心。**

---

## 五、装在哪（目录导航）

> **本仓库只包含文档**；模型与权重（合计约 40 GB）不随仓库分发，需按各项目官方说明自行下载。
> 文档在本机与仓库里的对应关系如下：

| 本机 `D:\AI\MusicAi\` | 本仓库 |
|---|---|
| `0-项目总表.md` | `README.md`（本文件） |
| `0-总说明.md` | `docs/总说明.md` |
| `0-GitHub选型排查-2026-10-12.md` | `docs/选型排查-2026-10-12.md` |

本机的落地目录结构：

```
D:\AI\MusicAi\
├── 0-项目总表.md            ← 功能 / Star / 评分 / 小主机可行性
├── 0-总说明.md              ← 全部项目的使用总说明
├── 0-GitHub选型排查-2026-10-12.md   ← 第一轮 GitHub 选型体检报告
│
├── 【分离 · 本次新装】
│   ├── UVR5\                 ← ★ 官方图形界面（v5.6 Roformer BETA，模型已预置）
│   └── VocalSeparator\       ← 脚本/网页版，与 UVR5 硬链接共享同一批模型
│
├── 【人声 · 已有】
│   ├── RVC\                  ← 变声 / 翻唱
│   ├── DiffSinger\           ← 音符级歌声合成 + OpenUtau
│   ├── SoulX-Singer\         ← 零样本歌声合成 + 翻唱
│   └── YingMusic-Singer\     ← 零样本歌声合成 + 编辑
│
├── 【整首歌生成】
│   ├── ACE-Step\             ← ★ 主力：歌词 → 整首歌
│   └── HeartMuLa\            ← 歌词 + 标签 → 音乐
│
├── 【音效 / 音频生成】
│   ├── StableAudio3\         ← 文生音乐（medium / large）
│   ├── StableAudioOpen\      ← 文生音频（轻量）
│   ├── TangoFlux\            ← 文生音效
│   ├── Woosh\                ← 文生 / 视频→音效
│   ├── MOSS-TTS\             ← 语音 + 音效（含 MOSS-SoundEffect v2）
│   └── MMAudio\              ← 视频/文本 → 音效
│
└── 【实时 / 探索性】
    └── MagentaRT\            ← 实时流式音乐生成（本机可用，小主机不可用）
```

---

## 六、评分口径说明

「评分」不是 Star 数的搬运，而是按 **本机（RTX 4070 Ti SUPER）实际可用性** 给出的：

- **效果 50%** —— 产出质量在同类中的位置（例如 BS-Roformer 在人声分离上 SDR 领先 Demucs 数个 dB）
- **成熟度 30%** —— 文档、更新频率、许可清晰度、能否 Windows 一键跑
- **易用性 20%** —— 有无中文界面 / 一键脚本 / 批量能力

所以会出现「Star 高但评分不是最高」的情况：
例如 **RVC（38.7k★）** 因为训练流程偏重、门槛高，评分 9.0；
而 **ACE-Step（13.4k★）** 因为许可证最宽松、效果接近 Suno v5、有官方 Windows 便携包，评分 9.2。

---

## 七、许可证提示（商用前必看）

| 许可 | 项目 | 可否商用 |
|---|---|---|
| **MIT** | UVR5、VocalSeparator、RVC、ACE-Step、Stable Audio 3、Stable Audio Open、MMAudio | ✅ 可商用 |
| **Apache-2.0** | SoulX-Singer、DiffSinger、MOSS-TTS、MagentaRT、Woosh | ✅ 可商用 |
| **非商用** | **TangoFlux**（权重 CC-BY-NC） | ❌ 仅个人/研究 |
| **未声明** | **YingMusic-Singer** | ⚠️ 商用前先联系作者 |
| **待确认** | HeartMuLa | ⚠️ 以仓库 LICENSE 为准 |

> 另外提醒：**用这些工具处理别人的商业歌曲**，产出物仍然是原版权方的作品，公开发布有侵权风险；自己练手/研究一般没问题。
