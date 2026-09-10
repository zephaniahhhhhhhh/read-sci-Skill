# Three-stage output contracts

## Common header

Begin every stage with paper identity, source language, covered sections, omitted or unreadable sections, and the glossary path/version read for this stage. Preserve source section and page anchors wherever practical.

## Stage 1

Use this order:

1. `论文定位`: One direct sentence stating setting, method, problem, and intended outcome.
2. `Abstract 中文翻译`.
3. `Introduction 中文翻译`.
4. `Related Work / Background 中文翻译`, following the paper's actual headings.
5. `研究问题与贡献`: Problem, importance, gap, proposed approach, and author-claimed contributions.
6. `术语对照`: Original term, abbreviation, Chinese translation, domain, and contextual definition.
7. `先验知识总结`: Organize mechanisms, theories, consensus, tasks, metrics, criteria, and assumed concepts in Chinese.
8. `来源边界`: Separate paper statements, paper-grounded inferences, and external additions.
9. `术语库更新`: Added, reused, conflicted, and awaiting-confirmation counts.
10. `继续提示`: End with a natural sentence such as `第一部分已完成。你可以回复“继续”“下一部分”“继续进行”等任意表达继续意图的话，我将进入第二部分：Methods、Experiments 与 Results。`

Do not include full source-language paragraphs in Stage 1 unless needed to explain a disputed translation.

## Stage 2

For every source paragraph use:

`[Section | page | paragraph identifier]`

**Original**

Complete source paragraph.

**中文翻译**

Complete corresponding Chinese translation.

Optionally add one short `段落作用` line when it materially helps navigation. Never place multiple source paragraphs above a combined translation.

After paragraph pairs, use this order:

1. `方法流程与变量解释`.
2. `实验与证据表`: Experiment question, comparison, metric, main result, and support judgment.
3. `实验设置原文汇总`: Source-language text only, grouped as Dataset/Cohort, Preprocessing, Implementation Details, Hardware/Software, Hyperparameters, Training Protocol, Evaluation Metrics, and Statistical Analysis. Preserve locations and write `未报告` for missing categories.
4. `术语库更新`.
5. `继续提示`: End with a natural sentence such as `第二部分已完成。你可以回复“继续”“下一部分”“接着来”等任意表达继续意图的话，我将进入第三部分：Discussion、Conclusion 与局限性总结。`

## Stage 3

Use this order:

1. `Discussion 中文翻译`.
2. `Conclusion / Future Work 中文翻译`.
3. `一句话结论`.
4. `直白结论`: What was done, data and conditions, comparator, size of improvement, and practical meaning.
5. `局限性`: Separate `作者明确承认` and `基于设计识别`.
6. `证据强度`: Claim, rating, and reason.
7. `这篇论文没有证明什么`.
8. `后续研究方向`.
9. `术语库更新`.

Avoid converting exploratory findings into confirmatory conclusions. Distinguish statistical significance, effect size, and practical or clinical significance.

## Long papers

If a stage exceeds a practical response length, split only at subsection boundaries, label each part `Stage N - Part X/Y`, preserve order, and state which subsection will continue. Do not advance to the next stage without the user's request.

When a split stage is incomplete, interpret `继续` and equivalent phrases as continuing the next part of that same stage. Only a completed stage may advance to the next stage. Do not append a next-stage invitation until the current stage's final part is complete.
