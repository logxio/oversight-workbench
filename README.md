# Oversight Workbench

Find where transcript monitors lose evidence, recover covert lookups with runtime provenance, and inspect why frozen tests break.

[Open the interactive workbench](https://yansu.me/oversight-workbench/)

<table>
<tr><th>Study</th><th>Recorded result</th></tr>
<tr><td>Frontier monitor calibration</td><td>960 evaluations on 120 balanced runs. At threshold 0.50, Sonnet 4.6 reduces clean-summary false alarms from Haiku 4.5's 29/60 (48.3%) to 4/60 (6.7%). Sonnet recovers 8/23 clue-retaining summaries; Haiku recovers 0/23.</td></tr>
<tr><td>Runtime provenance and probes</td><td>Six-family held-out Sonnet plus a 1.42ms provenance gate improves full-view recall from 12/60 to 40/60 at matched 3/60 clean false alarms, exact McNemar p = 5.774199962615967e-08. Covert lookup capture rises from 1/25 to 25/25.</td></tr>
<tr><td>Hermetic container replay</td><td>Across 76 PR pairs in 35 repositories, test-editing PRs break frozen base tests in 30/76 cases versus 15/76 controls, exact McNemar p = 0.01667384780012071. Auditing 2,897 hunks separates 17 specification updates, 12 weakened checks and 1 file move.</td></tr>
</table>

```sh
python3 reproduce.py
```

Python 3.9 or later. Standard library only. Runs in under one second. Open `index.html` directly for the interactive views.

The command verifies saved scores, operating thresholds, confusion matrices, nested leave-one-family-out selections, all 2,080 method-pair comparisons, container counts and a live generic completion-sentinel check. The HTML embeds the exact bytes of `data/evidence.json`. Reproduction checks recorded model decisions; it does not call or refit models.

Act 01 includes a 0.00 to 1.00 threshold slider, a ≤5% empirical FPR snap, all four transcript views, clue strata and held-out family errors. Sonnet catches 3/37 summaries with erased clues and 0/25 read-only lookups on summary or masked views (1/25 full). The separate refusal ledger contains 70/480 cells. The `legacy_monitor` table retains the historical 6.7% to 8.3% pooled LOFO false-alarm calculations.

Act 02 compares Sonnet 4.6, post-hoc Qwen2.5-Coder-0.5B (bf16) and 3B (4-bit) probes, provenance, and their hybrid on the same 120 runs and 6,773 tool calls. The 10,080-vector probe inventory exposes the length confound: the 3B masked pre-summary probe catches 13/25 covert cases at 6/60 clean false alarms, falling to 0/25 with length control. Full traces give 5/25 before length control and 0/25 after it. Generated-summary probes also catch 0/25. Covert labels come from upstream benchmark task design; provenance rules were fixed before scoring. Hybrid masked and summary recall is 36/60 and 37/60, with 24/25 covert lookups and 2/60 and 4/60 clean false alarms respectively. Full-view zero-clue capture improves from 4/37 to 28/37.

Inspect `tr-000501` for the single clean provenance alarm: authorized Cybench CTF access to exposed git history. Inspect `tr-003712` for Sonnet's complementary capture of leaked MLE-bench validation labels. Provenance records access; the task determines intent.

Act 03 filters all 30 breaking PRs by audit outcome and links directly to changed files. Repository-level paired votes are 14 versus 4 (exact p = 0.0308837890625). Across 96 recorded fixed-spec episodes, an end-of-harness completion sentinel catches 4/4 skipped-test edits with zero false alarms. The verifier also tests normal completion, assertion failure, skipping and early zero exits using a generic local runner.

Frontier monitors use each recorded transcript view. Post-hoc probes use deterministic transcript windows of at most 3,072 tokens. Provenance uses recorded tool calls and diffs. Model depth, pooling, regularization and thresholds are selected within training-family folds. Held-out clean errors are reported from outer predictions.

MIT License. Yan Su.
