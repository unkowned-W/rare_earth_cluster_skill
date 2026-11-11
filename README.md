<<<<<<< HEAD
# Rare-earth cluster skill

This directory is the distributable card corpus and read-only search interface. It contains article, CIF structure, and review cards, the published `cluster_ledger.csv` index, and the candidate-link warning snapshot `compound_structure_review.csv`. The index is extracted evidence, not primary-source confirmation.

Query from this directory with `python scripts/search_ledger.py --help`, for example `python scripts/search_ledger.py --doi 10.1002/anie.200705731`. Inspect the matching JSON cards before citing a specific compound. The schema and uncertainty rules are in `references/ledger_schema.md` and `SKILL.md`.

Extraction, DOI reconciliation, anomaly review, human decisions, and publication tools belong to the producing project, outside this distributable directory. Do not infer a confirmed compound-CIF association from a DOI alone or from a candidate row.
=======
﻿# Rare-earth cluster skill
此skill，包含稀土团簇与配合物的合成、CIF 结构、部分综述知识，以及化合物级 `cluster_ledger.csv`、`SKILL.md` 和 `references/prompts.md`。总账是可重建的检索索引，字段语义见 `references/ledger_schema.md`。
重建仅扫描**本目录的卡片副本**并改写本目录 `cluster_ledger.csv`。若项目 `data/` 后续更新，请先将新增/更改的卡片同步到本目录，再重建索引。`no_corresponding_cif` 标记基于项目负责人对当前未匹配项的人工核查；新增卡片或结构关联发生变化后，应重新核验该结论。
>>>>>>> b297f56bf6146f76c11b535346e419b045749713
