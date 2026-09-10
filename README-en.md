```
# read‑sci — Three‑Stage Scientific‑Paper Reading & Interpretation Skill
`read‑sci` is an agent skill for researchers: read, translate and critically interpret academic papers in three controlled stages, maintaining a reusable Excel terminology glossary for consistent term translation across multiple papers.

## Features
1. Supported input formats: PDF, Word(DOCX), PPTX, HTML, JATS‑XML, LaTeX, Markdown, RTF, plain text, scanned documents (OCR quality depends on your agent platform).
2. Three‑stage workflow
   - **Stage 1: Background & prior knowledge**: Translate abstract, introduction and related‑work sections; extract research questions, research gaps and paper contributions; summarize domain background knowledge and extract terminology entries.
   - **Stage 2: Methods, experiments & results**: Paragraph‑wise bilingual source‑and‑Chinese translation; parse datasets, inclusion criteria, baselines, metrics, ablation studies and statistical outputs; preserve raw experiment‑setting block in source language.
   - **Stage 3: Discussion, conclusion & limitations**: Translate discussion and conclusion sections; rate evidential support for main claims; separate author‑stated limitations vs limitations inferred from study design; explicitly state what the paper **does NOT prove** and suggest plausible future research directions.
3. Automatic shared glossary: `academic‑glossary.xlsx` auto‑created alongside `read‑sci.md`. Human‑curated translations take highest priority and will never be silently overwritten.

## Repository Layout
```

ReAd/
├─ read‑sci.md                 # Main skill definition
├─ README‑zh.md
├─ README‑en.md
├─ agents/
│  └─ openai.yaml
├─ references/
│  ├─ glossary‑contract.md
│  └─ output‑contracts.md
└─ scripts/

```
> ⚠️ The `references` sub‑folder must sit in same directory as `read‑sci.md`. Missing it will cause runtime error.

## Quick Start
### Basic invocation (glossary auto‑generated next to skill file)
```

read‑sci paper.pdf

```
Execution starts automatically at **Stage 1**.
After finishing each stage, use continuation phrases to proceed:
> Supported triggers: `继续`, `下一部分`, `继续进行`, `next`, `go on`, `proceed`.

### Override glossary path (for platforms with broken relative‑path resolution)
If glossary file is generated in unexpected directory, pass explicit file location:
```

read‑sci paper.pdf glossary_path="/home/user/my‑terms/my‑glossary.xlsx"

```

## Glossary sheet `academic‑glossary.xlsx`
Auto‑generated in skill directory. Column specification:

| Column | Description |
|---|---|
| Original term | Source‑language technical term |
| Domain | Research domain context |
| 人工首选译名 | Human‑curated preferred Chinese translation. **Never auto‑overwritten by skill** |
| 机器建议译名 | Machine‑suggested candidate translation |
| 生效译名 | Effective output translation: uses human preferred value if present; otherwise falls back to machine suggestion |
| Occurrence count | Cumulative term occurrence counter |
| Source paper | Paper from which this term was first extracted |
| Last updated date | Timestamp of last modification |
| Status | `Pending` / `Confirmed` |

> Newly extracted terms default to `Pending`. Manually set status to `Confirmed` after review.

## Evidence labels in output
Three labels distinguish information provenance:
- `[原文陈述]` Content directly stated by paper authors
- `[基于原文的推断]` Reasoned inference derived from paper content
- `[外部补充知识]` External background knowledge outside the paper; will cite sources or mark as `一般性解释（未外部核验）` when external verification is unavailable.

> `译注：` marks translation notes for ambiguous wording.

## Troubleshooting
1. **`academic‑glossary.xlsx` is not generated?**
   - Runtime lacks write permission for skill folder. Glossary entries will be reported as pending updates without file output.
2. **Glossary file appears in wrong folder?**
   - Agent platform cannot resolve relative path against skill file. Workaround: use `glossary_path=` parameter to supply absolute path.
3. **Error: cannot load contract files**
   - Missing `references/` folder. Clone full repository, do not copy only `read‑sci.md`.

## Notes
- Quality for scanned documents depends on platform OCR accuracy. Skill will warn when extraction fails; please supply editable document.
- The skill faithfully reproduces original paper statements and does not auto‑correct errors in source papers. Paper claims do not represent views of this skill.
- This skill is for research‑assistance only; not medical, legal or financial professional advice.

## License
MIT
```