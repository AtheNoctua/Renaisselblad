# Contributing to Renaisselblad

感谢你帮助整理和延续经典 Hasselblad H 系统。项目接受文档、解析工具、Ghidra 标注、协议观察、测试记录与补丁定义。

## 先选择贡献类型

- **Research finding**：新的地址、字段、函数、协议或跨版本关系。
- **Tooling**：解析、提取、重建、校验或报告生成工具。
- **Hardware result**：明确机身、数字后背、附件与固件版本的实机记录。
- **Patch**：从指定基底可重复生成的差异，而不是来源含混的完整二进制。
- **Documentation**：把既有证据整理成可复现报告。

## 每次提交需要包含

1. 输入文件名、版本、大小与完整 SHA-256；
2. 目标硬件组合与当前固件版本；
3. 工具版本和精确命令；
4. 修改组件、地址范围或符号；
5. 输出文件大小与 SHA-256；
6. 预期行为与实际观察；
7. 静态、虚拟、实机测试分别处于什么状态；
8. 恢复基底、恢复过程与结果。

## 状态用词

- `VERIFIED`：已有可复现工具结果或明确实机记录。
- `EXPERIMENTAL`：候选实现已存在，覆盖矩阵仍在扩充。
- `RESEARCH`：定位、推断或验证设计阶段。
- `ARCHIVED`：保留复盘，但退出当前发布路线。

请把“看起来像”“应该是”放在推断部分，把地址、字节、哈希、交叉引用和测试输出放在已确认部分。

## Pull request 流程

1. 从最新 `main` 创建范围单一的分支。
2. 使用小写、清晰的分支名，例如 `docs/hbf-format` 或 `tool/cim-parser`。
3. 保持功能补丁、显示资源变体和实验探针彼此独立。
4. 运行相关工具测试、容器校验和 Markdown 链接检查。
5. 更新报告、manifest、测试矩阵和 `CHANGELOG.md`。
6. 在 PR 描述中填完验证与恢复栏目。

## 文件与发布命名

推荐格式：

```text
renaisselblad-h4d60-cb141208-hm1632-compat-v0.1.0-beta.1.hbf
h4d60-cb141208-hm1632-compat.patch.yaml
hasselblad-h4d-body-cb141208.sha256
```

`FINAL`、`NEW` 或只有 `V2/V3` 的名字无法表达基底、功能和状态，发布时请改用可排序的版本号及 manifest。

## Commit 风格

```text
docs: document HBF component table
tool: validate legacy CIM checksum
test: add H4D60 and HM 16-32 hardware result
patch: add reproducible HM 16-32 compatibility delta
```

## Review 标准

审核首先检查结论是否与证据范围一致，其次检查工具能否从记录的输入重建结果，最后检查文档、输出哈希和恢复结果是否匹配。
