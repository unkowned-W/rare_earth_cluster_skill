# Rare-earth cluster skill（全项目卡片）

此目录仿照 `high_quality_samples/`，包含合成、CIF 结构、综述卡片的独立副本，以及化合物级 `cluster_ledger.csv`、`SKILL.md` 和 `references/prompts.md`。原始 `data/` 卡片未改动。总账是可重建的检索索引，字段语义见 `references/ledger_schema.md`。

从项目根目录运行：

```powershell
python rare_earth_cluster_skill/scripts/search_ledger.py --element Gd --min-nuclearity 20 --limit 10
python rare_earth_cluster_skill/scripts/search_ledger.py --doi '10.1002/anie.200705731'
python rare_earth_cluster_skill/scripts/build_ledger.py --check
python rare_earth_cluster_skill/scripts/build_ledger.py
```

重建仅扫描**本目录的卡片副本**并改写本目录 `cluster_ledger.csv`。若项目 `data/` 后续更新，请先将新增/更改的卡片同步到本目录，再重建索引。`no_corresponding_cif` 标记基于项目负责人对当前未匹配项的人工核查；新增卡片或结构关联发生变化后，应重新核验该结论。
