# CISEval

CISEval is a small, lightweight evaluation setup for poking at how models change their trust-related signals—mainly things like confidence and disclosure—when you tweak incentives.

The rough idea is to keep the task itself mostly the same, but change the incentive framing (usually via different system prompts), then see how the model’s tone and self-presentation shift. We try to hold prompts (and rough “truth targets”) fixed so that changes in confidence/disclosure aren’t just because the model is answering a different question.

At a high level:

* Run the *same prompts* under different incentive regimes
* Look at how confidence and disclosure signals change
* Optionally sanity-check this with a tiny human trust probe (A/B style) to see which answers people *feel* more inclined to trust

This is exploratory and intentionally a bit scrappy.

## Quickstart (Python 3.11-ish)

```bash
pip install -r requirements.txt

python scripts/run_generation.py
python scripts/run_scoring.py
python scripts/run_report.py

streamlit run demo/streamlit_app.py
streamlit run trust_probe/app.py
```

Nothing fancy here—just run things in order.

## What’s in the box

* **Generation**
  `scripts/run_generation.py` runs all `prompt × incentive regime` combinations and dumps raw model outputs to `runs/raw/` (JSONL).

* **Scoring**
  `scripts/run_scoring.py` adds simple confidence / disclosure scores plus a few diagnostics, written to `runs/scored/`.

* **Reporting**
  `scripts/run_report.py` produces a rough markdown summary (`reports/summary.md`) and a couple basic plots.

* **Demo viewer**
  `demo/streamlit_app.py` lets you flip through the same prompt answered under different regimes.

* **Trust probe**
  `trust_probe/app.py` is a very small A/B rater UI. It just appends votes to `trust_probe/data/ratings.csv`. This is meant as a quick gut-check, not a real study.

## Known limitations / caveats

These are mostly intentional:

* **“Truth held constant” is fuzzy**
  Correctness isn’t actually guaranteed. Prompts only have a lightweight `truth_target`, so answers can still drift.

* **Scoring is heuristic**
  Confidence and disclosure are detected with pattern matching and rules, not a trained or calibrated rater.

* **Incentives are prompt-level only**
  Incentives are implemented via system prompts, and models don’t always follow those cleanly or consistently.

* **The trust probe is noisy**
  The rater UI is minimal on purpose. Results are directional at best—useful for exploration, not conclusions.



