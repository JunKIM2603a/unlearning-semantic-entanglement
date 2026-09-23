# Scripts

Planned entry points:

```text
scripts/
├── train_base.py
├── make_forget_split.py
├── extract_representations.py
├── build_similarity_bins.py
├── run_unlearning.py
├── evaluate.py
├── run_relearning.py
└── make_main_figures.py
```

Keep research logic reusable under `src/`; scripts should mostly parse configuration and call library functions.

The first implementation goal is an end-to-end smoke test, not full baseline coverage.
