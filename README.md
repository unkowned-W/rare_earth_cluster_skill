# Rare-earth cluster skill

This directory is the distributable card corpus and read-only search interface. It contains article, CIF structure, and review cards, the published `cluster_ledger.csv` index, and the candidate-link warning snapshot `compound_structure_review.csv`. The index is extracted evidence, not primary-source confirmation.

Query from this directory with `python scripts/search_ledger.py --help`, for example `python scripts/search_ledger.py --doi 10.1002/anie.200705731`. Inspect the matching JSON cards before citing a specific compound. The schema and uncertainty rules are in `references/ledger_schema.md` and `SKILL.md`.

Extraction, DOI reconciliation, anomaly review, human decisions, and publication tools belong to the producing project, outside this distributable directory. Do not infer a confirmed compound-CIF association from a DOI alone or from a candidate row.
