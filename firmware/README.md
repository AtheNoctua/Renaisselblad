# Firmware catalog conventions

本目录保存固件 **manifest、来源链接、哈希和提取记录**。大型原始包、解码整包和构建产物通过 GitHub Release 资产分发，Git 历史保留可审阅的元数据。

## 命名规则

```text
hasselblad-h4d-body-cb141208.hbf
hasselblad-h4d-body-cb141208.plain.hbf
h4d-body-cb141208-component-08-kind84-sub0-base08000800.bin
renaisselblad-h4d60-cb141208-hm1632-compat-v0.1.0-beta.1.hbf
```

名称使用小写 ASCII 与连字符，并包含机型、原厂版本、功能、项目版本和发布状态。外观变体使用独立字段，例如 `stock-logo` 或 `h7dx-logo`。

## Manifest 最低字段

```yaml
schema: renaisselblad.firmware/v1
id: hasselblad-h4d-body-cb141208
vendor: Hasselblad
device:
  class: body
  family: H4D
vendor_version: CB141208
container:
  format: HBF
  format_version: 7
artifacts:
  official:
    filename: hasselblad-h4d-body-cb141208.hbf
    size: 401784
    sha256: 3026e2b7e33f8e45381e1cd195d492c420a5527ff144f9e1ab2be588e5c1db82
    distribution: github-release
source:
  kind: official-package
  url: https://example.invalid/vendor-source-record
  retrieved: 2026-09-03
extraction:
  tool: tools/hbf_tool.py
  command: python tools/hbf_tool.py extract INPUT.hbf OUTPUT_DIRECTORY
```

示例中的 `example.invalid` 是 schema 展示值；正式 manifest 应记录实际来源页面或本地档案编号。

## 三种固件状态

- `official`：保存下载来源与原始 SHA-256；
- `plaintext`：由指定工具从 official 派生，记录派生关系；
- `generated`：由补丁或构建脚本产生，链接补丁 manifest 和测试记录。

三者分别命名和记录，避免把解码容器、提取组件与可刷写成品统称为“明文固件”。

测试要求见 [../docs/TESTING.md](../docs/TESTING.md)。
