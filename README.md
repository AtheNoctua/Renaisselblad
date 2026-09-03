# Renaisselblad

**Renaissance + Hasselblad — keeping classic Hasselblad H-system hardware useful through documented firmware research and community engineering.**<br>
**Renaissance + Hasselblad —— 通过可复现的固件研究与社区协作，让经典哈苏 H 系统继续工作。**

[中文](#中文) · [English](#english-overview)

> **仓库状态 / Repository status:** Initial public organization. Only entries linked to a report, manifest, reproducible tool, or release are treated as published results.<br>
> 公开资料正在整理；只有链接到报告、清单、可复现工具或 Release 的条目才视为已发布成果。

## 中文

### 项目简介

Renaisselblad 是一个由爱好者发起、AI 辅助的哈苏 H 系统固件研究项目。名字由 **Renaissance** 与 **Hasselblad** 组合而成，表达“哈苏复兴”的愿望：把旧机型的固件结构、升级链路和硬件兼容行为整理成可复现、可验证、可继续推进的社区知识。

AI 用于加速格式识别、二进制差异分析和反编译工作。历史材料会在复核输入、SHA-256、修改差异及测试记录后分批发布。

## 项目状态 / Project status

| 方向 | 状态 | 当前证据边界 |
|---|---|---|
| H4D60 + HM 16-32 识别 | **VERIFIED — 实机** | 一套组合上消除 `Back not compatible`，卷片与释放通过测试 |
| H4D/H7DX 启动画面修改链路 | **VERIFIED — 实机** | 已完成刷写与启动显示验证 |
| HBF、旧 CIM、H6D `VHABCIM` 容器研究 | **VERIFIED — 工具** | 本地工具可重复解析，报告和工具正分批整理 |
| 扩展数字后背兼容性 | **EXPERIMENTAL** | 正在建立机身 × 后背 × 固件版本测试矩阵 |
| Average 测光模式 | **RESEARCH** | 当前实机仍循环 `CenterW / Spot / CenterSpot` |
| AF 与高速快门研究 | **RESEARCH** | 固件静态分析与跨版本比较阶段 |
| `AF_TIMING_P0_TEST` | **ARCHIVED** | 已归档的失败探针；恢复基底经实机确认 |

以上状态针对记录中的硬件和固件组合，不自动扩展到同系列的全部机身与数字后背。

### 状态标签

| 标签 | 含义 |
|---|---|
| `VERIFIED` | 有可复现工具结果或明确的实机记录 |
| `EXPERIMENTAL` | 候选实现已生成，测试覆盖仍在扩充 |
| `RESEARCH` | 分析、定位或假设验证阶段 |
| `ARCHIVED` | 保留用于复盘，退出当前发布路线 |

### 研究范围

- HBF、传统 CIM 与 H6D `VHABCIM` 固件容器；
- Phocus 的固件识别、校验、传输与设备升级链路；
- H4D/H4X 数字后背兼容逻辑；
- AF、测光模式、高速快门与机身—后背协议；
- 手柄 LCD、后背显示资源和启动画面；
- 固件提取、差分、重打包、静态验证和硬件测试流程。

## 仓库导航 / Repository map

| 路径 | 内容 |
|---|---|
| [`docs/`](docs/) | 项目状态、固件结构、测试方法和研究文档索引 |
| [`firmware/`](firmware/) | 固件命名、哈希与 manifest 规范 |
| [`patches/`](patches/) | 功能补丁、外观变体和实验版本的组织规范 |
| [`tools/`](tools/) | 解析、提取、校验和构建工具入口 |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Issue、报告、代码和实机测试的提交要求 |
| [`CHANGELOG.md`](CHANGELOG.md) | 仓库与正式发布记录 |

功能补丁、外观修改和失败实验分别归档，避免把启动图变化当成功能兼容性证据。大型构建产物适合放入 [GitHub Releases](https://github.com/AtheNoctua/Renaisselblad/releases)；Git 历史主要保存工具、manifest、补丁定义、报告和 SHA-256。

## 快速开始 / Quick start

1. 从 [`docs/README.md`](docs/README.md) 选择研究入口。
2. 在 [`docs/FIRMWARE_FORMATS.md`](docs/FIRMWARE_FORMATS.md) 确认容器类型与提取流程。
3. 按 [`firmware/README.md`](firmware/README.md) 记录原始输入、来源、大小和 SHA-256。
4. 按 [`docs/TESTING.md`](docs/TESTING.md) 分开执行静态、虚拟与实机测试。
5. 提交发现或补丁前阅读 [`CONTRIBUTING.md`](CONTRIBUTING.md)。

推荐分析顺序：

```text
container → validate/decode → extract component → choose architecture/base
          → Ghidra → diff → rebuild → validate → hardware test → recovery record
```

Ghidra 用于分析已经提取的代码组件；HBF/CIM 的容器识别、解码与组件切分由对应解析工具完成。

### 最低复现记录

每一项发布结果至少应包含：

- 原始固件版本、文件大小与完整 SHA-256；
- 目标机身、数字后背及附件组合；
- 修改的组件、地址范围和差异文件；
- 输出文件 SHA-256；
- 静态、虚拟与实机测试结果；
- 恢复基底、恢复步骤和恢复结果。

### 参与项目

欢迎协助复现实验、补充兼容矩阵、标注 Ghidra 函数、整理 Phocus 日志、审阅解析工具，或把旧分析记录改写成带证据路径的报告。请使用仓库的 Issue 模板，并让每项结论可以从明确的输入重新得到。

## English overview

Renaisselblad is a community-led, AI-assisted firmware research project for classic Hasselblad H-system hardware. The name combines **Renaissance** and **Hasselblad**: a practical effort to keep these cameras useful by documenting firmware formats, update paths, and compatibility behavior in a reproducible form.

Digital-back recognition has been restored on one recorded H4D60 + HM 16-32 setup: the `Back not compatible` message disappeared, and winding and release passed hardware testing. Universal digital-back compatibility remains experimental and is tracked through an explicit hardware matrix.

Research also covers HBF/CIM containers, the Phocus update path, autofocus, metering modes, high-speed shutter behavior, and display resources. Results are labelled `VERIFIED`, `EXPERIMENTAL`, `RESEARCH`, or `ARCHIVED` according to their evidence.

Contributions are welcome in reproducible testing, body/back compatibility records, Ghidra symbol annotation, Phocus log analysis, documentation, and parser review. Please include the base version and SHA-256, target hardware, exact change, test procedure, observed result, and recovery result.

Start with the [documentation index](docs/README.md) and [contribution guide](CONTRIBUTING.md).

---

Renaisselblad is an independent community research project and is not affiliated with Hasselblad. Product names are used to identify the hardware covered by the research.
