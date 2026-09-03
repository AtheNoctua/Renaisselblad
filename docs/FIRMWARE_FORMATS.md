# Firmware formats and analysis workflow

Status: `static-verified`<br>
Last reviewed: 2026-09-03

本文给出仓库使用的固件分层与术语。详细字段报告发布后会从这里链接。

## 一、传统机身 HBF

H3D/H4D/H4X/H5D 一代的机身升级包常以 `.hbf` 分发：

- 文件以 `VHAB` 开头；
- 外层保存构建信息、流状态、明文长度、CRC32 和组件表位置；
- 解码后得到组件表及一组反向链接的块描述符；
- 描述符记录目标地址、长度、数据位置与前一描述符；
- 同一包可包含多个目标节点和 prepare/data/finalize 阶段。

因此 HBF 是一份多组件升级配方，而不是单块连续 ROM。

## 二、R366/R520 传统数字后背 CIM

旧式数字后背 CIM 采用固定 `0x210` 字节头：

- 头部与载荷使用不同固定 XOR 值；
- 解码标识为 `HASSELBLAD FIRMWARE IMAGE`；
- 头中保存加法校验、组件数量、类型、版本与尺寸；
- 各组件从 `0x210` 起顺序拼接。

类型号的语义应通过升级分派函数、总线记录和跨版本样本命名，避免只凭尺寸猜测。

## 三、H6D VHABCIM

H6D 公共升级包使用 `VHABCIM`：

- 明文公共头和私有文件表；
- 内容采用 AES-128-CBC；
- 完整性使用带固定 salt 的 MD5 规则；
- 外层包含升级入口、Linux rootfs、U-Boot 和子系统版本清单；
- rootfs 内继续包含升级脚本及机身、传感器、电源、USB、触控等子节点固件。

H6D 的公开包属于由 Sensor Unit 协调的一体化系统升级包，与旧 CIM 的平面组件列表是不同世代。

## 四、Phocus 与目标设备的职责

```text
firmware package
  → Phocus parses and validates
  → Phocus compares model/component versions
  → device enters update/service state
  → chunks are transferred with waits and retries
  → target bootloader/updater erases and programs flash
  → finalize, reboot and re-enumeration
```

Phocus 负责识别、校验、协调与传输；目标设备中的 bootloader/updater 执行最终擦除、写入与启动切换。传统 H 系统可由数字后背桥接机身组件；H6D 则由 Sensor Unit 向内部子节点分发。

## 五、Ghidra 工作流

Ghidra 的输入应是已经从容器提取的代码组件：

```text
preserve original hash
  → validate/decode container
  → extract components and manifest
  → identify ELF / Intel HEX / raw / data resource
  → select CPU, endianness and image base
  → import into Ghidra
  → vectors, strings, xrefs, call graph and version diff
```

常见配置：

| 对象 | Ghidra 导入方式 | 处理器/基址 |
|---|---|---|
| H4/H5 ARM 机身组件 | Raw Binary | Cortex-M，按描述符，常见 `0x08000800` |
| H6 CBM/CBC | Intel HEX 或转 raw | Cortex-M，保留 HEX 基址 |
| R366/R520 主程序 | Raw Binary | ARMv5T，已分析样本使用 `0x30100000` |
| H6 Linux daemon | ELF | 让 Ghidra 保留 section/import 信息 |
| EEPROM、字体、位图 | Data/resource | 按结构分析，不作为 CPU 代码 |

Cortex-M 向量表的第二字通常是 Reset Handler；地址最低位表示 Thumb 状态，建立函数时使用清除最低位后的实际地址。

## 六、修改与验证边界

容器有效、Phocus 接受、传输完成、设备启动和摄影功能正常是五个不同结果。项目对它们分别记录：

1. 外层长度和校验；
2. 组件边界与未修改区域；
3. 重打包 round-trip；
4. Phocus 识别和传输结果；
5. 冷启动、供电、识别、释放、曝光、存储与恢复结果。

进一步的记录格式见 [TESTING.md](TESTING.md)，固件命名和 manifest 规则见 [../firmware/README.md](../firmware/README.md)。
