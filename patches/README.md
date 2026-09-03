# Patch organization

本目录保存可重建的差异、补丁 manifest、说明和测试记录。完整固件输出作为 Release 资产，并通过 SHA-256 与这里的定义对应。

## 分类

```text
patches/
  compatibility/   # 数字后背、附件和协议兼容
  cosmetic/        # 启动画面、字体和显示资源
  experimental/    # 探针和研究候选
  withdrawn/       # 已确认缺陷的历史实验与复盘
```

一个补丁只表达一个主要目的。兼容逻辑和启动图署名采用两个独立补丁，使功能测试结果不受外观差异干扰。

## 状态

```text
research
probe
experimental
hardware-tested
stable
withdrawn
```

## Patch manifest 示例

```yaml
schema: renaisselblad.patch/v1
id: h4d60-cb141208-hm1632-compat
version: 0.1.0
status: hardware-tested
target:
  body: H4D-60
  vendor_firmware: CB141208
base:
  filename: hasselblad-h4d-body-cb141208.hbf
  sha256: 3026e2b7e33f8e45381e1cd195d492c420a5527ff144f9e1ab2be588e5c1db82
patch:
  format: xdelta3
  filename: h4d60-cb141208-hm1632-compat.xdelta3
  sha256: 64_HEX_CHARACTERS
output:
  filename: renaisselblad-h4d60-cb141208-hm1632-compat-v0.1.0.hbf
  sha256: 64_HEX_CHARACTERS
  variant: stock-logo
verification:
  static: pass
  hardware_record: tests/hardware-results.yaml
recovery:
  verified_restore: true
```

每个补丁还应给出修改组件、地址范围、修改前后字节或函数、生成命令以及未覆盖的测试项。测试格式见 [../docs/TESTING.md](../docs/TESTING.md)。
