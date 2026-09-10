# read‑sci Skill
> Three‑stage scientific‑paper reading, translation and critical interpretation skill with auto‑managed Excel terminology glossary.
三阶段科研论文阅读翻译解析 Skill，自动维护可复用 Excel 术语库。

> Skill identifier: `read‑sci`
> ❗Do **NOT** only copy `read‑sci.md`；the `references/` folder is mandatory dependency.
> 不要只拷贝 `read‑sci.md`，`references` 文件夹为运行依赖，必须完整下载。

## Repository structure
ReAd/
├─  agents/
│   └─  openai.yaml
├─  references/
│   ├─  glossary‑contract.md
│   └─  output‑contracts.md
├─  scripts/          # empty folder, contains .gitkeep
├─  read‑sci.md
├─  README.md
├─  README‑zh.md
└─  README‑en.md



## Quick Usage
Basic invoke（glossary auto‑generated next to `read‑sci.md`）
```bash
read‑sci your‑paper.pdf

Custom glossary path (fix relative‑path resolution issue on some platforms):
read‑sci your‑paper.pdf glossary_path="/absolute/path/to/your‑glossary.xlsx"

Continue keywords after finished each stage：
`继续` / `下一部分` / `继续进行` / `next` / `go on` / `proceed`