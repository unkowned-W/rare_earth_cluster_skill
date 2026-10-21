# Prompt patterns and initial evaluation

Use these as **user-facing test prompts** or adapt them to the task. The instruction in `SKILL.md` remains authoritative; prompts do not themselves supply chemical facts.

## Grounded lookup

> 请基于本目录 cards 查找 DOI `{doi}` 中化合物 `{label}` 的合成条件、核数与结构依据。逐项给出 JSON 路径及字段，区分正文/SI 提取与 CIF 推导；缺失条件写“卡片未给出”，不要补全。

## Matched structure audit

> 对 CCDC `{ccdc}` / refcode `{refcode}`，用合成卡、结构卡和 `cluster_ledger.csv` 核对是否属于同一个具体化合物。说明核数的来源、可用的原子/键数据、候选结构模块的证据等级，以及不能从该 CIF 卡推出的结论。

## Comparative reasoning

> 在本地卡片里选出符合 `{elements_or_motif}` 且总金属核数至少 `{n}` 的实例，比较配体/模板、反应条件、结构描述和性能。每条结论附化合物级来源；解释筛选范围与不可直接比较的测量条件。综述只用于带限定条件的背景解释。

## Hypothesis, not recipe

> 我希望探索 `{target}`。请从卡片寻找最相近的先例，提出 2–3 个有明确证据边界的设计假设、可能失败模式与需要核验的原始文献/CIF 信息。不要把相关性说成因果，也不要保证产物或性能。

## Contradiction / abstention

> 对 `{claim}` 做证据审计：哪些卡片直接支持、哪些只是综述归纳或结构算法提示、哪些与之冲突或缺少必要字段？若无法证实，请明确弃答并给出最小核验清单。

## First-pass evaluation of Cluster_agent

1. Freeze a small test set of questions *before* looking at model answers: identifier lookup; multi-compound DOI disambiguation; missing CIF match; missing atom/bond graph; review scope transfer; cross-card comparison; unsupported synthetic prediction. Include both answerable and deliberately unanswerable items. Avoid putting expected answers inside the query.
2. Run the same questions against a baseline model without this skill and with this skill plus cards, holding model and other settings fixed. Record retrieved paths, response, time, and whether external browsing was used. If browsing differs, do not attribute gains solely to cards.
3. Independently verify sampled assertions against the actual card fields and, where feasible, original article/SI/CIF. Score at the **claim** level: correct compound linkage, synthesis fidelity, structure interpretation, scope-aware review use, citation traceability, calibrated abstention; note hallucinations and overconfident statements separately. Do not score prose fluency as domain knowledge.
4. Report counts/denominators and representative failures; distinguish improved retrieval/grounding from genuine generalization. This is an initial check, not a benchmark proving novel chemistry or experimental reproducibility.

## Ledger-first ligand and analog retrieval

> 请查找使用 `{ligand}` 的 Gd 化合物。先用 `--element Gd --reagent` 检索，再打开少量候选合成卡核实试剂是否承担配体角色。选择一个明确的 `compound_key` 用 `--similar-to` 找相似候选，并解释相似性信号不能证明同构或相同反应机理。

## Missing crystallographic evidence

> 对 `{compound_key}` 核对 `structure_availability`。如果为 `no_corresponding_cif`，区分“项目负责人已人工确认无对应 CIF”的项目状态与“CCDC 数据库没有记录”这一尚未由账本证明的说法。列出合成卡中可用的文章报告结构描述，同时说明哪些晶体学信息无法从结构卡验证。
