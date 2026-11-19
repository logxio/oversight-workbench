https://yansu.me/oversight-workbench/

Recompute every statistic in 0.05 seconds with Python 3.9+ standard library on Linux, macOS, or Windows (no third-party packages required):

```sh
python3 reproduce.py
```

On Windows, `python reproduce.py` also works. The script reads `data/evidence.json`, the exact JSON embedded in the interactive workbench.

| Finding | Measured result | Source |
| :- | :- | :- |
| Monitor views at <=5% in-family FPR | Across 600 Claude Haiku 4.5 monitor evaluations (5 views on 120 balanced 6-family runs) plus 400 reference records, completion summaries catch 3.3% (2/60) of positive runs vs 13.3% (8/60, 0% in-sample FPR) on git diff logs, 15.0% (9/60) on full traces, and 21.7% (13/60) on tool-masked traces | [Monitor data](data/evidence.json) |
| Cross-family LOFO holdout FPR drift | Transferring <=5% FPR thresholds across 6 task families breaks holdout false-alarm control (pooled 6.7% to 8.3% FPR, reaching 41.7% [5/12] on terminal-bench-2 and 66.7% [4/6] on swe-bench-verified) | [LOFO holdout table](data/evidence.json) |
| Frozen base-test container replay | Across 76 paired PR container builds in 35 repositories (extending ImpossibleBench, Zhong et al., 2025), test-editing PRs fail frozen pre-change base tests twice as often as same-repository controls (30/76 = 39.5% vs 15/76 = 19.7%, exact McNemar p=0.0167; excluding github/gh-aw p=0.041; repo-level 14 vs 4, p=0.031) | [Container replay data](data/evidence.json) · [Picchio sandbox replay](https://yansu.me/picchio/) |
| Parser retry loops & queue-value stopping | Across 229,580 retry attempts (162,506 Qwen3.8 27B + 67,074 Qwen3 Coder 480B) plus 228 full-event Gemma 4 31B traces (1,988 silent parser rejections), queue-value stopping resolves +43.2% to +78.9% more recoverable tasks at compute budgets <=30% | [gemma4-queue-value](https://github.com/logxio/gemma4-queue-value) |
| Confidence-gated ARC-AGI-3 control | Across all 183 ARC-AGI-3 levels on 4 LLM backbones, mean score rises from 3.18 to 58.70 at 0.413x action cost across 825 paired runs (694 wins, 131 ties, 0 losses) | [arc-agi-3-paper](https://github.com/logxio/arc-agi-3-paper) |

The script recalculates all five monitor views on the 120 balanced 6-family runs and 69 SWE-bench Verified runs, all six leave-one-family-out holdout folds, and all three paired container tests (full 76 pairs, excluding `github/gh-aw`, and repository-level sign test).
