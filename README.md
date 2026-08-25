# dsh-research-skills

面向硬件设计研究的两套 DSH Skill（研究方法 SOP），可直接被 DSH 的 skill 系统加载使用。

## 包含的技能
- **official-design-research** — 官方推荐设计研究 SOP：按官方参考设计/数据手册/应用笔记给出原理图级设计建议，每条结论带来源标注。
- **pdf-datasheet-extraction** — PDF 资料研读 SOP：从数据手册/参考设计 PDF 提取文字/表格/参数并给出可引用页码，含 CJK 乱码与图形处理。

## 用法
将对应技能目录（`skills/official-design-research/` 或 `skills/pdf-datasheet-extraction/`）加入 DSH `skills/` 目录，DSH 即会识别其 `SKILL.md`。技能内的 `<项目根>`、`<pymupdf解压目录>` 等占位符按你的环境替换。

## 说明
- 内容为通用方法 SOP，不含具体项目数据。
- 每个技能一个 `SKILL.md`（frontmatter：name/description）。
