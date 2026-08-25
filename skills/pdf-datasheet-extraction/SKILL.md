---
name: pdf-datasheet-extraction
description: PDF 数据手册/资料研读 SOP——从 PDF 提取文字/表格/参数并给出可引用页码，含 CJK 乱码与图形处理。
---

# Skill: PDF 资料研读 SOP

## 适用场景
需要从 PDF（芯片数据手册、参考设计原理图、集成手册）中提取文字、表格、参数，且必须给出可引用的页码/章节定位。

## 环境
- Python 3.x + PyMuPDF（已解压 wheel，无需安装，`sys.path` 插入解压目录即可）
- 用法：
  ```python
  import sys
  sys.path.insert(0, r"<pymupdf解压目录>")
  import pymupdf
  doc = pymupdf.open(r"<pdf路径>")
  page = doc[i]
  txt = page.get_text("text")   # 提取整页文本
  ```
- 数据手册副本统一放在项目目录：`<项目根>/datasheets/`（ASCII 文件名）

## 步骤
1. **定位**：先用 `get_toc()` 或逐页搜索关键词（正则 + 页码记录），找到目标章节。
2. **提取**：整页/段落提取；表格用 `get_text("text")` 分行解析。
3. **引用规范**：每条结论写成「结论 —— 来源：<文件名>，第 N 页（PDF 页码，注意封面偏移）」。PDF 内页码与物理页偏移：用 get_text 查看页脚页码再换算。
4. **中文路径**：若文件路径含中文，先复制成 ASCII 名再打开（避免编码乱码）。
5. **CJK 特殊 PDF**（如立创EDA导出、无 ToUnicode 的字体）：
   - `get_text` 乱码时，读内容流 `page.read_contents()`，正则提取 `<十六进制> Tj / [...] TJ` 字符串；
   - 按 UTF-16-BE 解码：`bytes.fromhex(h).decode('utf-16-be')`；
   - 图形：`page.get_drawings()` 取矩形/线段，聚类共线线段识别虚线框；
   - 渲染成图：`page.get_pixmap(matrix=pymupdf.Matrix(3,3)).save(png)` 供视觉校验（勿依赖读图）。
6. **输出**：研究笔记写入项目对应章节文件，结论后附 [来源]。

## 注意
- 不要把中文路径直接嵌进 python 命令（PowerShell→python 编码会损坏）；先复制为 ASCII 名。
- python 结果直接写 UTF-8 文件再用 read 工具读，避免控制台中文乱码。
