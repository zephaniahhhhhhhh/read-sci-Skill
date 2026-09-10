# read‑sci Skill
> Three‑stage scientific‑paper reading, translation and critical interpretation skill with auto‑managed Excel terminology glossary.
三阶段科研论文阅读翻译解析 Skill，自动维护可复用 Excel 术语库。

## Purpose / 项目目的
### 中文
该 skill 的目的是三段式拆分论文，降低初学者的阅读压力。

- **第一阶段**：精确拆分 Abstract、Introduction、Related Work 等章节；补充对应领域基础知识，对齐梳理论文创新点。
- **第二阶段**：精读 Method、Experiment、Result 等章节并做分析；忠于原文做一比一双语翻译，长段落会合理切分；同时检查章节内部细节不一致问题，也可辅助论文初稿审阅。
- **第三阶段**：精读 Discussion、Conclusion 等章节；忠于原文一比一翻译；汇总实验存在缺陷、未来改进方向，复盘论文核心创新。

本工具会自动构建本地 Excel 术语库。论文内出现的专业单词与固定术语，经过联网核验后录入术语库。
> 术语库为使用者本地独立，不同研究方向之间术语库互不共享，防止术语库被污染；每一条新增术语都需要使用者人工审阅确认。
> 前期会带来少量操作成本，但随着术语库持续扩充，能够有效拓展你的专业词汇，长期助力科研学习。

如需修改翻译目标语言，可以直接编辑 `read‑sci.md` 配置。本 Skill 仅作为基础范式，欢迎在此基础上改造出属于你自己的工具。

### English
This skill splits academic papers into three‑stage workflow to lower the reading burden for beginners.

- **Stage 1**: Precisely parse Abstract, Introduction, Related Work and other context sections; supply domain background knowledge and sort out the paper’s core innovations.
- **Stage 2**: Deep‑dive into Methods, Experiments and Results with analysis. Provide faithful paragraph‑by‑paragraph bilingual translation without altering original meaning. Long paragraphs will be reasonably split. Inconsistent details within this section will be inspected; this feature can also assist draft‑paper review.
- **Stage 3**: Read Discussion and Conclusion sections faithfully with side‑by‑side translation. Summarize experimental limitations and potential future improvements, and recap the paper’s key innovations.

A local Excel terminology glossary will be built automatically. Professional words and fixed technical terms extracted from papers will be added after online cross‑check.
> Glossaries remain local and isolated for each user. Glossaries for different research directions will not be shared with each other to prevent terminology contamination. Every newly‑extracted term requires manual human review.
> There is minor overhead at early usage, yet as the glossary grows, it expands your technical vocabulary and benefits your long‑term research‑learning progress.

If you want to change target translation language, modify settings directly inside `read‑sci.md`. This skill serves only as a foundational template; feel free to adapt and build your own variant upon it.

---

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
