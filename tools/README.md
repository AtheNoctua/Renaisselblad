# Tools

本目录用于存放容器解析、组件提取、差异、重打包和校验工具。

## 工具要求

每个命令行工具应提供：

- `--help` 与输入/输出说明；
- 明确的容器版本和适用样本；
- 输入 SHA-256 或结构 guard；
- 非零错误退出状态；
- 只写入显式输出路径；
- JSON/CSV manifest；
- 合成 fixture 或可公开的最小测试；
- round-trip 与损坏输入测试。

## 推荐子目录

```text
tools/
  hbf/           # VHAB HBF inspect/unpack/extract/repack
  cim/           # legacy CIM inspect/decode/extract/repack
  h6d/           # VHABCIM validate/decrypt/rootfs extraction
  ghidra/        # repeatable import and xref scripts
  verification/  # hash, manifest and release checks
```

## 统一输出

解析工具输出的 manifest 至少包含：

```json
{
  "input": "firmware-file.hbf",
  "input_sha256": "64_HEX_CHARACTERS",
  "format": "HBF",
  "valid": true,
  "components": []
}
```

工具生成的所有绝对路径在提交前改为仓库相对路径或参数占位符，以便其他环境复现。
