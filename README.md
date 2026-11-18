https://yansu.me/oversight-workbench/

Recompute the results in two seconds with Python 3.9+ on Linux, macOS or Windows. No packages to install:

```sh
python3 reproduce.py
```

On Windows, `python reproduce.py` also works. The script reads `data/evidence.json`, the exact JSON embedded in the interactive page.

| Finding | Measured result | Source |
| --- | --- | --- |
| Monitor summaries | At ≤5% false alarms, summary recall falls from 68.3% to 3.3%; masked traces retain 21.7% | [Monitor data](data/evidence.json) |
| Modified tests | 30/76 patches pass modified tests while failing frozen base tests, versus 15/76 controls; exact McNemar p=0.0167 | [PR 1401](https://github.com/github/gh-aw/pull/1401) · [PR 1513](https://github.com/github/gh-aw/pull/1513) |
| Parser loops | 229,580 trajectories; stopping at a 30% call budget solves 43.2% more tasks | [Replay data and stopping rule](https://github.com/logxio/gemma4-queue-value) |
| Action gate | ARC-AGI-3 score rises from 3.18 to 58.70 across 183 levels at 0.413x actions | [Action controller and results](https://github.com/logxio/arc-agi-3-paper) |

The script also recalculates all five monitor views on 120 matched runs and 69 SWE-bench runs, including six leave-one-benchmark-out folds. Holdout thresholds use clean runs from the other five benchmarks. Hover over a number for its denominator, threshold and source.
