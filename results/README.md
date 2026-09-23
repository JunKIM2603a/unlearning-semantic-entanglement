# Results

This directory stores **small, reviewable research outputs**.

Recommended layout:

```text
results/
├── figures/
├── tables/
└── README.md
```

Do not commit:

- raw per-batch logs
- full checkpoints
- large tensor dumps
- local experiment-tracker directories

Those are ignored through `.gitignore`.

## Main figure target

The first decisive figure should compare retain utility degradation across:

- low similarity
- mid similarity
- high similarity

for each unlearning method, with uncertainty once multiple seeds are available.

A second key figure should show controlled relearning / recovery curves.
