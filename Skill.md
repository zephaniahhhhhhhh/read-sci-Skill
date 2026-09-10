---
name: read-sci

description: Read, translate, and critically interpret scientific papers and research materials in three user‑controlled stages while maintaining a shared editable Excel terminology glossary. Use for PDF, Word/DOCX, PowerPoint/PPTX, HTML, JATS/XML, LaTeX, Markdown, RTF, plain text, scanned documents, or other reliably readable paper formats when the user wants Chinese background translation, paragraph‑level source‑language/Chinese methods and results, plain‑language conclusions and limitations, or consistent terminology reused across papers.

---

# read-sci

## Overview

Read one scientific paper as a controlled three‑stage workflow. Translate into Chinese, preserve traceability to the source, distinguish paper claims from added knowledge, and treat the shared Excel glossary as the authoritative terminology memory.

## Defaults

- Use Chinese as the target and explanatory language.
- Preserve the paper's original language for bilingual passages and verbatim experiment settings.
- Use `./academic‑glossary.xlsx` as the default shared glossary. This path is relative to the location of this skill file. The glossary file will be automatically created in the same folder as this skill if it does not yet exist.
- Stop after the requested stage. Start with Stage 1 unless the user explicitly requests another stage.
- Re‑read the glossary before every stage so manual edits made between stages take effect.
- For PDF inputs, use the available PDF skill to extract, render, and verify layout‑sensitive content.
- For Word, DOC, DOCX, ODT, or RTF inputs, use the available Documents skill to inspect structured text and rendered pages; include tracked text, tables, captions, footnotes, and figures that belong to the paper.
- For PPT or PPTX inputs, use the available Presentations skill to inspect every relevant slide, speaker notes when available, tables, charts, figures, equations, and references. Map slide groups to the three stages by research function rather than slide order alone.
- For HTML, JATS/XML, EPUB, LaTeX, Markdown, plain text, scanned images, or another paper format, extract or render content with an appropriate available tool while preserving headings, paragraph order, captions, citations, equations, and source locations. If reliable extraction is impossible, report the limitation and request an accessible export instead of guessing.
- For the `.xlsx` glossary, use the available Spreadsheets skill and its bundled runtime. Do not substitute an unapproved spreadsheet library. If the glossary file does not exist at the relative path, create a new empty glossary workbook with the required columns. If the runtime is unavailable, finish the reading stage, preserve the pending glossary entries, and report pending glossary updates.
- Read [references/glossary‑contract.md](references/glossary‑contract.md) before reading or updating the glossary.
- Read [references/output‑contracts.md](references/output‑contracts.md) before producing a stage.
- Optional input parameter: `glossary_path`. If provided, overrides the default relative‑path glossary location, for environments where relative‑to‑skill‑file resolution is unavailable.

## Prepare the Paper

1. Resolve glossary file path:
   - If user supplies parameter `glossary_path`, use this user‑provided full/relative path.
   - Otherwise use default: `./academic‑glossary.xlsx` relative to this skill file.
2. Identify title, authors, year, venue, DOI when present, source language, page count, and available sections.
3. Map variant headings by function rather than name:
   - Abstract, Introduction, Background, Literature Review, Related Work -> Stage 1.
   - Methods, Materials and Methods, Methodology, Study Design, Implementation, Evaluation, Experiments, Findings, Results -> Stage 2.
   - Discussion, Implications, Limitations, Future Work, Conclusion -> Stage 3.
4. For PDFs, inspect enough rendered pages to verify reading order, columns, tables, figures, equations, footnotes, and OCR quality. Do not trust extracted text alone when layout affects meaning.
5. Report missing, unreadable, or ambiguous content. Never reconstruct absent text from expectation.
6. Preserve section, subsection, page, figure, table, equation, and citation identifiers whenever available.

## Advance Between Stages

- Infer continuation from conversational intent rather than requiring one exact command.
- After a completed Stage 1, treat concise requests such as `继续`, `继续进行`, `继续输出`, `下一部分`, `下部分`, `继续下一部分`, `接着`, `接着来`, `往下`, `开始下一部分`, `进入第二部分`, `方法部分`, `实验部分`, `可以`, `好的`, `行`, `continue`, `go on`, `next`, `next part`, `proceed`, and close paraphrases as requests to begin Stage 2.
- After a completed Stage 2, interpret the same continuation intent as a request to begin Stage 3.
- Tolerate punctuation, quotation marks, minor typos, mixed Chinese/English, and polite wording. Match the intent, not only the listed strings.
- If the current stage was split into multiple parts and is not yet complete, a continuation request continues the next part of that same stage. Advance stages only after the current stage is complete.
- If the user explicitly names a stage or section, honor that target. If the user says `继续解释...`, `继续修改...`, or otherwise clearly refers to a local subtask, perform that subtask instead of advancing.
- Do not ask for confirmation when the continuation intent and current stage are clear. After Stage 3, state that the three‑stage reading is complete rather than restarting.

## Apply Translation Rules

- Translate faithfully without strengthening, weakening, or silently correcting the authors' claims.
- On first use, write `中文译名（Original term, ABBR）`; then use the glossary's effective Chinese consistently.
- Preserve formulas, symbols, variables, units, model names, datasets, scales, drug names, gene names, and citation numbers.
- Mark uncertainty as `译注：...` and explain the ambiguity briefly.
- Separate three evidence classes: `[原文陈述]`, `[基于原文的推断]`, and `[外部补充知识]`.
- Base prior‑knowledge summaries on the paper and its cited context. For any knowledge added beyond the paper, consult authoritative sources when available, cite them, and label the addition explicitly. If external verification is unavailable, mark it as `一般性解释（未外部核验）` and omit time‑sensitive, medical, legal, financial, or other high‑stakes claims.
- Describe correlation as correlation unless the design supports causality.
- Explain tables, figures, and equations near the relevant section; do not omit evidence solely because it is visual.

## Stage 1 - Background and Prior Knowledge

1. Re‑read the glossary and resolve terminology using its precedence rules.
2. Translate Abstract, Introduction, Related Work, Background, and equivalent research‑context sections into Chinese only.
3. State in one direct sentence what the paper uses, in which setting, to solve which problem.
4. Summarize the research question, importance, existing gap, proposed approach, and claimed contributions.
5. Produce a Chinese prior‑knowledge summary covering theories, mechanisms, field consensus, standard tasks, metrics, clinical criteria, or concepts the paper assumes.
6. Include a concise in‑response bilingual term table, then merge extracted terms into the shared glossary.
7. End with a short invitation explaining that the user may use any natural continuation phrase, such as `继续`, `下一部分`, or `继续进行`, to enter Stage 2.
8. Stop and wait for continuation intent.

## Stage 2 - Methods, Experiments, and Results

1. Re‑read the glossary before translating so newly edited user terms override previous suggestions.
2. Translate Methods, Experiments, Evaluation, Findings, and Results paragraph by paragraph. For every paragraph, show the complete original paragraph followed immediately by its Chinese translation.
3. Preserve paragraph order. Split only when a source paragraph is too long, and label the split parts.
4. Explain study population or datasets, inclusion criteria, inputs, outputs, labels, preprocessing, model flow, formulas, variables, baselines, data splits, metrics, ablations, statistical tests, and reported effect sizes when present.
5. Summarize each major experiment as question -> comparison -> metric -> result -> whether the evidence supports the claim.
6. Collect the experiment settings into a separate source‑language‑only block. Do not translate or paraphrase that block. Preserve its source locations.
7. Merge new terms and usage records into the glossary.
8. End with a short invitation explaining that the user may use any natural continuation phrase to enter Stage 3, then stop and wait for continuation intent.

## Stage 3 - Discussion, Conclusions, and Limits

1. Re‑read the glossary before translating.
2. Translate Discussion, Implications, Limitations, Future Work, Conclusion, and equivalent sections into Chinese.
3. Give a one‑sentence conclusion and a direct account of what was done, under which data and conditions it worked, compared with what, and by how much.
4. Separate author‑stated limitations from limitations inferred from design, data, evaluation, statistics, reproducibility, external validity, and deployment risk.
5. Rate each main claim as sufficiently supported, partly supported, insufficiently supported, or overstated, with a short reason.
6. State explicitly what the paper did not prove and list credible next research steps.
7. Merge any final terminology and usage records into the glossary.

## Maintain the Shared Glossary

- Glossary file location: `./academic‑glossary.xlsx`, relative to this skill file. If the file does not exist on first run, create a blank workbook with required columns: Original term, Domain, 人工首选译名, 机器建议译名, 生效译名, Occurrence count, Source paper, Last updated date, Status(Pending / Confirmed). Pending=待确认，Confirmed=已确认. If the glossary file is created in unexpected folder, explicitly pass parameter `glossary_path` with your target file path.
- Treat `人工首选译名` as user‑owned. Never overwrite it unless the user explicitly asks to change that cell.
- Compute `生效译名` from `人工首选译名` when nonblank; otherwise use `机器建议译名`.
- Prefer an exact original‑term and domain match. Fall back to a confirmed general‑domain term before generating a new candidate.
- Keep separate rows when the same source term has distinct domain meanings.
- Append new terms as `Pending`; never replace an existing approved translation silently.
- Sort populated terms case‑insensitively by the full original term, then domain. Place non‑Latin source terms after A‑Z terms.
- Update source, occurrence count, and dates without erasing prior provenance.
- Rebuild `待确认` and `打印版` after every glossary update.
- If the workbook is locked or cannot be safely written, preserve it and report the pending updates instead of risking corruption.

## Quality Gate

Before completing each stage, confirm that section coverage is complete, bilingual paragraphs remain paired, terminology follows the latest glossary, numerical claims match the source, evidence labels are present, and no inferred or external claim is presented as the authors' statement.
