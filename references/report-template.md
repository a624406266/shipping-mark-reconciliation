# Shipping-mark Markdown report template

Use this structure. Replace all angle-bracket placeholders and omit empty optional rows; never leave template tokens in the delivered report.

```markdown
# <项目号> 箱唛核对差异报告

## 核对文件

- Excel 原始内容：`<Excel 文件名>`
- PDF 供应商定稿：`<PDF 文件名>`
- 核对依据：以 `<权威来源>` 为原始依据，对照 PDF 全部 `<页数>` 页及所有重复箱唛版面。

## 内容逐项核对

| 核对项目 | Excel 是怎么样的 | PDF 是怎么样的 | 是否有差异 | 差异是什么 |
|---|---|---|---|---|
| <字段名称> | `<Excel 值或状态>` | `<PDF 值、状态及适用页/版面>` | <规定分类> | <差异、范围或“一致”说明> |

## PDF 文件级异常

<没有异常时写“未发现额外页面、错单页面、缺页或重复版面异常。”>

| 核对项目 | Excel 是怎么样的 | PDF 是怎么样的 | 是否有差异 | 差异是什么 |
|---|---|---|---|---|
| <页数、项目编号、字体或重复版面等> | <Excel 依据> | <PDF 实际情况> | <规定分类> | <异常范围和影响> |

## 最终结论

<按工作流中的结论规则写一句明确结论。>

需要供应商修改的内容：

1. <按严重程度排列的修改项；没有修改项时写“无”。>

建议供应商：<删除错页、修正数据或排版、嵌入字体、重新导出并复核等可执行建议。>

## 核对说明

- 轻微格式差异：<列出或写“无”>。
- 不判定为差异的辅助信息：<列出 Excel 中未要求印刷的 ORDER QTY、CTN 等，或写“无”>。
- 待人工确认或未完成检查：<列出限制，或写“无”>。
```

## Reporting rules

- Each row must show both sources, a classification, and a concise explanation. Do not list only the mismatching value.
- Identify the exact PDF page and repeated-face scope for any page-specific or instance-specific defect.
- Keep confirmed defects separate from auxiliary-information gaps and harmless presentation differences.
- When there is no file-level anomaly, retain the section with the explicit no-anomaly statement; the anomaly table may be omitted.
- Link the generated Markdown file in the final response. Do not link temporary renders, extraction files, or QA intermediates.
