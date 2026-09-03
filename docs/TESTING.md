# Testing and hardware validation

固件研究需要把静态检查、虚拟检查与实机结果分开。测试记录使用观察事实，不用一个“成功”覆盖所有层级。

## 测试层级

### 1. Static

- 输入 SHA-256 与 manifest 匹配；
- 容器长度、CRC/checksum/MD5 通过；
- 组件数量、顺序、目标地址和尺寸符合预期；
- 字节差异只出现在声明范围；
- 解包—重打包 round-trip 结果一致。

### 2. Virtual or emulated

- CPU 类型、端序、基址和向量表合理；
- 修改后的控制流可达；
- 无越界跳转、错误常量池或损坏资源索引；
- 模拟覆盖范围及未模拟外设明确记录。

### 3. Hardware

- 冷启动与重复启动；
- 机身向数字后背供电；
- 机身、后背、取景器和镜头识别；
- 快门、卷片、释放与曝光；
- AF、测光和菜单循环；
- CF、FireWire/USB 与 Phocus 连接；
- 休眠、唤醒和关机；
- 原厂基底恢复。

## 实机记录模板

```yaml
schema: renaisselblad.hardware-test/v1
date: 2026-09-03
tester: github-handle
artifact:
  filename: example.hbf
  sha256: 64_HEX_CHARACTERS
base:
  vendor_version: CB141208
  sha256: 64_HEX_CHARACTERS
hardware:
  body: H4D-60
  back: H4D-60
  attachment: HM 16-32
  viewfinder: HV90X-II
software:
  phocus: 3.x
  operating_system: Windows
checks:
  cold_boot: pass
  back_power: pass
  back_detection: pass
  shutter_release: pass
  exposure: pass
  storage: not-tested
recovery:
  base_reflash: pass
notes:
  - Record exact display messages and timing here.
```

## 兼容矩阵规则

矩阵中的每一行只代表该行的硬件与固件组合。重复测试增加 `runs`，换机身、换后背或换固件时新增一行。失败记录保留原始输出，并链接到复盘报告。

## 发布门槛

- `experimental`：静态检查通过，并提供恢复基底。
- `hardware-verified`：至少一套明确组合完成核心实机项目及恢复测试。
- `stable`：覆盖计划中的主要组合，且构建与恢复均可重复。

补丁的组织和状态字段见 [../patches/README.md](../patches/README.md)。
