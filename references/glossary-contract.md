# Shared glossary contract

## Workbook

Use the default workbook at `F:\学习\3硕士\4.论文相关\论文术语库\academic-glossary.xlsx` unless the user supplies another path. Import the existing workbook before any translation stage and preserve its workbook structure and formatting.

## Sheets

- `使用说明`: Explain editable fields, precedence, statuses, and printing.
- `术语库`: Store the authoritative flat terminology table.
- `待确认`: Show unresolved candidates and conflicts; rebuild it from the main table after updates.
- `使用记录`: Record one row per paper/term usage event.
- `打印版`: Present a compact A-Z learning and printing view.

## 术语库 columns

Keep these columns and meanings:

1. `原文术语`: Canonical full source-language term.
2. `缩写`: Abbreviation or acronym.
3. `生效译名`: Formula or derived value selecting the user preference first.
4. `人工首选译名`: User-owned editable translation; leave blank for new machine candidates.
5. `机器建议译名`: Proposed Chinese translation.
6. `学科领域`: Domain needed to disambiguate the term.
7. `中文释义`: Concise Chinese definition in the paper's context.
8. `使用说明`: Context restrictions, prohibited translations, or usage notes.
9. `别名`: Source-language spelling variants, singular/plural forms, or aliases.
10. `状态`: `待确认`, `已确认`, or `有歧义`.
11. `首次来源`: First paper identifier.
12. `最近来源`: Most recent paper identifier.
13. `使用次数`: Positive integer count.
14. `首次记录日期`: Date value.
15. `最近更新日期`: Date value.
16. `排序键`: Lowercased, trimmed canonical term used for stable sorting.

Use `=IF(D2<>"",D2,E2)` as the row logic for `生效译名`, adjusted to the actual row. Treat yellow input cells in `人工首选译名` as user-editable and preserve them during rebuilds.

## Resolution precedence

Resolve a term in this order:

1. Exact canonical term + exact domain + nonblank `人工首选译名`.
2. Exact canonical term + `通用` domain + nonblank `人工首选译名`.
3. Exact canonical term + exact domain + `已确认` effective translation.
4. Exact canonical term + `通用` domain + `已确认` effective translation.
5. Exact alias or abbreviation match, provided the surrounding context disambiguates it.
6. Create a new `待确认` candidate.

Do not use an ambiguous abbreviation without checking its expanded form and local context.

## Merge and sorting

- Normalize comparisons with Unicode normalization, trimmed whitespace, and case-insensitive matching; retain the paper's display capitalization.
- Use original term + domain as the logical key.
- Never overwrite nonblank `人工首选译名` during automatic updates.
- If a suggested translation conflicts with an existing row, retain the existing row and flag the case as `有歧义`.
- Sort populated rows by `排序键`, then `学科领域`; keep blank template rows at the bottom.
- Update the print sheet after sorting with only `原文术语`, `缩写`, `生效译名`, `中文释义`, and `学科领域`.

## Usage records

Record paper title or stable identifier, year, section, page when available, original term, effective Chinese, domain, event date, and note. Append records; do not rewrite history.

## Safe writing

Inspect the workbook before editing, write updates to a temporary export, verify formulas and all five sheets, then replace or save the intended workbook only after verification. If the file is open or locked, do not force replacement.
