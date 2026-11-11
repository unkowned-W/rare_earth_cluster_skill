# Prompt patterns and initial evaluation

Use these as **user-facing test prompts** or adapt them to the task. The instruction in `SKILL.md` remains authoritative; prompts do not themselves supply chemical facts.

## Grounded lookup

> 请基于本目录 cards 查找 DOI `{doi}` 中化合物 `{label}` 的合成条件、核数与结构依据。逐项给出 JSON 路径及字段，区分正文/SI 提取与 CIF 推导；缺失条件写“卡片未给出”，不要补全。

## Article-internal analogous synthesis

> 请查 `{doi}` 中化合物 `{target_label}`。如果卡片说它按另一化合物的方法制备，先在同篇文献 card 按 `compound_label` 精确定位所引用的基准化合物，并分别核对两者的 `synthesis`（必要时 SI）。按“基准步骤/文献明确更换的试剂和条件/目标化合物展开后的步骤”列出，仅在文献明确共享时沿用数值；每步标明证据来源与缺失/推断部分。如果标签、计量或参照链有歧义，不要编造完整配方。

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

> 对 `{compound_key}` 核对 `structure_availability`。若为 `ambiguous_local_cif_match`，查 `compound_structure_review.csv`，列出候选但不作唯一归属；若为 `no_local_cif_match`，仅说明当前 skill card 未能建立精确对应，不能声称数据库没有 CIF。引用文献 card 中已有的结构描述，区分其与 CIF 验证的晶体学信息。
