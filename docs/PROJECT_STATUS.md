# Project status

Last reviewed: 2026-09-03

本页记录项目现阶段的证据边界。单次硬件测试不会自动代表整个产品系列；每次新增结果都应写入明确的机身、数字后背、附件、版本和测试日期。

## Hardware-verified

### H4D60 + HM 16-32 recognition

- Body: H4D-60
- Body firmware base: CB141208 系列已验证基底
- Attachment: HM 16-32
- Observed result: `Back not compatible` 消失
- Functional checks: 卷片、释放通过
- Coverage: 当前记录对应一套实机组合

### Startup display resource workflow

- H4D/H7DX 机身启动图修改、重打包和刷写链路已经过实机验证。
- 外观变体与后背兼容功能在补丁目录中应分别发布。

## Static-verified

- HBF `VHAB` 容器的逐字节变换、长度、CRC32、组件表和块描述符。
- R366/R520 传统 CIM 的头部/载荷 XOR、加法校验和组件目录。
- H6D `VHABCIM` 的文件表、AES-CBC 内容、MD5 完整性及 rootfs 展开流程。
- Phocus 3.8.7 中固件更新入口、容器解析分支与异步 I/O 线索。

## Experimental

### Expanded digital-back compatibility

目标是建立可测量、可回滚的兼容策略，而不是用一个 `Universal` 文件名代替测试矩阵。每个候选版本应分别记录：

- 机身型号与机身固件；
- 数字后背/胶片后背/第三方后背型号；
- 供电、识别、释放、曝光与存储结果；
- Phocus 连接和原版恢复结果。

## Research

- Average 测光模式与手柄 LCD 的模式循环。
- H4D/H6D AF 状态机、扫描范围和等待参数。
- H6D 高速快门程序与 H4D/H5D 的差异。
- Phase One P 系列与 Leaf Aptus 的识别及触发协议。

## Withdrawn or archived

### AF_TIMING_P0_TEST

该探针曾使机身停留在 `Preparing digital back`，并影响后背上电。使用已验证基底重刷后，供电、识别与释放恢复。它保留为失败实验复盘，不进入 Release 资产。

## 下一轮公开整理顺序

1. 发布固件格式、Phocus 刷写链路和 Ghidra 工作流文档。
2. 发布 HBF/CIM 解析工具及合成测试样本。
3. 建立固件 manifest 和硬件测试矩阵。
4. 将 HM 16-32 成果整理为可从指定基底生成的补丁。
5. 将 Universal、AF、测光和高速快门研究按状态分别发布。
