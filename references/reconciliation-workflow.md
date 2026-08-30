# Excel-to-PDF shipping-mark reconciliation workflow

## 1. Establish the comparison set

- Resolve the exact Excel and PDF paths before extracting content.
- Derive the project identifier from the source content when possible; use filenames only as supporting evidence.
- Record the source filenames, Excel sheets/ranges inspected, PDF page count, and which source is authoritative.
- If the files appear to describe different projects, continue only far enough to document that file-level mismatch; do not silently select a seemingly matching page and ignore the rest of the PDF.

## 2. Inspect the Excel source

Use the Spreadsheets skill and its required read-only workflow.

- Inspect every populated sheet, relevant used range, formulas/displayed values, merged cells, comments, drawings, and embedded images.
- Render every relevant sheet or range. Workbook text extraction alone does not verify logos, compliance symbols, hierarchy, or print-layout notes.
- Capture, when present: carton dimensions, printing-side requirements, brand/series, SKU, description, item number, customer or supplier PO, outer-carton quantity, batch/date code, net and gross weight, company name, address, email, logos, compliance marks, order quantity, and carton count.
- Preserve identifiers exactly, including leading zeros, hyphens, spaces that are part of an identifier, and letter case where case may be meaningful.
- Classify each item as one of:
  - `箱唛正文`: content intended to appear on the carton mark;
  - `印刷要求`: instructions in Excel that define the expected output, such as four-side printing, logo placement, or reserving date-code space;
  - `订单辅助信息`: source metadata such as total order quantity or total carton count that is not shown as part of the mark body.

Do not call auxiliary information missing from the PDF a defect unless the Excel layout or a source note clearly requires it to be printed.

## 3. Inspect the supplier PDF

Use the PDF skill for metadata, extraction, rendering, and visual verification.

- Inspect metadata and total page count, then render every page at sufficient resolution to read small carton text.
- Extract text for search and structured comparison. If a page is scanned or extraction is incomplete, use OCR as supporting evidence, but visually confirm every reported discrepancy.
- On each page, record the page title/job identifier and the content of every repeated carton-face instance. Compare repeated instances with one another; a defect in only one of four copies is still a confirmed defect and its scope must be reported.
- Check text and numbers as well as logos, compliance symbols, line breaks, spacing, clipping, overlap, missing glyphs, unreadable fonts, and obvious font-substitution or non-embedded-font risk.
- Treat extra pages, pages belonging to another project, unexpected blank pages, and duplicated or omitted faces as file-level anomalies.

## 4. Compare in three layers

### Layer A: structured values

Compare every Excel item against every corresponding PDF instance. Identifiers, quantities, dates, batch codes, weights, addresses, and contact details require exact semantic agreement.

### Layer B: rendered presentation

Verify the structured comparison on the rendered workbook and PDF. Presentation can change meaning or printability: for example, `ZURU FRANCE33 rue` is a layout defect even when all words are present.

### Layer C: final coverage sweep

Before writing the conclusion, rescan all populated Excel items, all PDF pages, and all repeated faces. Confirm that every item appears in the report or is explicitly classified as auxiliary information.

## 5. Safe normalization and classifications

Never normalize identifiers, leading zeros, PO numbers, SKU values, item numbers, batch/date codes, or address components into a false match.

Allowed semantic interpretation is narrow:

- surrounding whitespace that does not affect readability may be ignored;
- equivalent unit capitalization such as `mm` and `MM` remains a `有轻微格式差异` rather than a content error;
- adding an unambiguous count unit such as `24` versus `24 PCS` may be `有轻微格式差异` when the quantity is unchanged;
- line-break or spacing changes are `有排版差异` when fields run together or readability is reduced;
- reordered repeated faces are not a difference when their content and required coverage are identical.

Use only these values in the `是否有差异` column:

- `无差异`: comparable content and presentation agree;
- `有内容差异`: both sources contain comparable values and they differ;
- `有排版差异`: the content may be present, but layout, spacing, clipping, overlap, or glyph rendering is defective;
- `有轻微格式差异`: semantic content agrees, but unit display, capitalization, or other harmless presentation differs;
- `信息缺口`: an expected comparable field exists on only one side;
- `不判定为差异`: Excel information is auxiliary and not required in the printed mark;
- `待人工确认`: extraction and visual evidence conflict, or the source is not reliably legible.

Do not report `核对无误` while any content difference, layout difference, information gap, file-level anomaly, or unresolved item remains.

## 6. Overall conclusion rules

- Any content difference, layout difference, or file-level anomaly: `存在差异，不能直接确认定稿。`
- No material difference, but one or more harmless format differences: `无内容差异，但存在轻微格式差异。`
- All comparable fields and layouts agree: `核对无误。`
- Any unresolved item: `存在待人工确认项，暂不能确认核对无误。`

Prioritize supplier actions: remove wrong pages, correct wrong values, repair unreadable or concatenated text, embed fonts, re-export, and recheck the replacement PDF.
