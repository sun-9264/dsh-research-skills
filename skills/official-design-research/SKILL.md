---
name: official-design-research
description: 官方推荐设计研究 SOP——对每个芯片给出按官方参考设计/数据手册/应用笔记的原理图级设计建议，每条结论带来源标注。
---

# Skill: 官方推荐设计研究 SOP

## 目标
对每个芯片给出「按官方推荐设计」的原理图级设计建议，每条细节注明参考来源（本地文件给路径+页码；联网资料给 URL+文档名+页码/章节）。

## 优先级（强制）
1. **官方参考设计 / 评估板原理图**（Reference Layout、EVM、DK、集成手册的 Reference Design 章节）—— 第一依据
2. **数据手册**的 Application/Recommended Operating Conditions/Typical Application 章节 —— 第二依据
3. **官方应用笔记 / 设计检查清单**（如 nPM1304 design checklist、TI SBAA/SBOA、Nordic 白皮书）—— 补充
4. **第三方总结**（仅当官方资料缺失，且必须注明"非官方"）

## 每个子系统的输出模板
1. 芯片选型确认（封装、后缀、与框图的对应）
2. 电源设计（供电轨、电压、去耦电容值/封装、上电时序）[来源]
3. 时钟设计（晶振型号/负载电容、内部时钟选项）[来源]
4. 接口连接（SPI/I2C/UART/QSPI 引脚到主控的接法、上拉、电平）[来源]
5. 模拟前端细节（ECG/PPG 特有的：输入滤波、RLD、LED 驱动拓扑、光电二极管接法、光路布局）[来源]
6. 关键 BOM（电阻/电容/电感/晶振 具体值+封装+推荐型号）[来源]
7. 布局要点（官方 layout guidance 的 3-5 条核心）[来源]
8. 与框图差异点/风险项（如框图写"SPI-NAND"但实际选 NOR；"磁力计待确定"；GH3020 资料缺失）
9. 参考文献清单（每个条目：文件名+页码 或 URL）

## 联网检索要点（资料不足时）
- 优先检索：芯片名 + "reference design" / "schematic" / "EVM user guide" / "application note"
- 官网下载页优先（ti.com、nordicsemi.com、u-blox.com、invensense.tdk.com、bosch-sensortec.com、goodix.com）
- 把关键结论与 URL 记录到项目 refs/ 目录的清单文件，正文只引用清单编号
- 半公开物料（如 GH3020）：公开资料可能只有 PR/简介；标注「官方完整资料待 NDA/待发」，基于公开信息给出设计要点并列出需官方确认项

## 交付
- 每章一个 md 文件存到项目目录：`<项目根>/0X_<子系统>.md`
- 结论逐条带 [来源: …] 标记；没有来源的推测必须显式标注【推断，待确认】
