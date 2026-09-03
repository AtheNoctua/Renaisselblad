# Documentation index

这里是 Renaisselblad 的文档入口。首页只保留项目定位和状态；具体结构、证据和测试记录放在本目录。

## 当前文档

| 文档 | 用途 |
|---|---|
| [PROJECT_STATUS.md](PROJECT_STATUS.md) | 已验证、实验、研究及归档路线 |
| [FIRMWARE_FORMATS.md](FIRMWARE_FORMATS.md) | HBF、传统 CIM、H6D `VHABCIM` 的结构概览 |
| [TESTING.md](TESTING.md) | 静态、虚拟与实机测试记录规范 |

## 后续报告的统一结构

每篇研究报告建议包含：

1. 结论与适用范围；
2. 输入样本、来源、大小和 SHA-256；
3. 分析方法与工具版本；
4. 字段、地址、函数或协议证据；
5. 可复现命令；
6. 验证结果；
7. 已确认事实、工程推断与待补证项目；
8. 输出、差异及恢复记录。

详细报告可以使用以下 front matter：

```yaml
---
schema: renaisselblad.report/v1
id: report-hbf-container
title: Hasselblad HBF Container Format
status: static-verified
models:
  - H4D
base_firmware: CB141208
input_sha256: 3026e2b7e33f8e45381e1cd195d492c420a5527ff144f9e1ab2be588e5c1db82
last_verified: 2026-09-03
---
```

## 状态词

- `hardware-verified`：明确设备组合上的实机记录；
- `static-verified`：容器、校验、代码或脚本结果可重复；
- `experimental`：候选实现存在，覆盖矩阵仍在扩展；
- `superseded`：已被后续版本替代；
- `withdrawn`：已确认存在缺陷，只保留复盘资料。
