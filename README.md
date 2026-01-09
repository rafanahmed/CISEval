# CISEval

CISEval is a lightweight **incentive-switching evaluation harness** for spotting *trust-signal distortion* in model outputs—primarily **confidence** and **disclosure**—while trying to keep **task correctness roughly constant** by holding prompts (and “truth targets”) fixed.

The idea: run the same set of prompts under different **incentive regimes** (different system prompts), then score outputs for confidence/disclosure signals, run simple diagnostics, and optionally collect a small **trust probe** (A/B rater UI) to see which regime’s answers people trust more.

## Quickstart (Python 3.11)

```bash
pip install -r requirements.txt

python scripts/run_generation.py
python scripts/run_scoring.py
python scripts/run_report.py

streamlit run demo/streamlit_app.py
streamlit run trust_probe/app.py
```

## What you get

- **Generation**: `scripts/run_generation.py` runs `prompt × regime` and writes JSONL to `runs/raw/`.
- **Scoring**: `scripts/run_scoring.py` computes confidence/disclosure + diagnostics into `runs/scored/`.
- **Reporting**: `scripts/run_report.py` writes `reports/summary.md` and a couple simple plots.
- **Demo viewer**: `demo/streamlit_app.py` shows outputs across regimes for a chosen prompt.
- **Trust probe**: `trust_probe/app.py` is a tiny rater UI that appends to `trust_probe/data/ratings.csv`.

## Limitations (by design)

- **Truth-fixed is approximate**: “correctness held constant” is not guaranteed; prompts have only a lightweight `truth_target`.
- **Heuristic scoring**: confidence/disclosure are scored via pattern matching, not a trained rater.
- **Prompt-level incentives**: incentives are implemented as system prompts; models may not follow them reliably.
- **Small rater probe**: the trust UI is intentionally minimal and noisy; it’s a quick signal, not a study.

