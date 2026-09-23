# Unlearning Semantic Entanglement

Similarity-stratified analysis of collateral damage and reversibility in machine unlearning under retain-forget semantic entanglement.

## Research question

**Does higher forget-retain semantic similarity lead to larger collateral damage and/or greater reversibility after machine unlearning?**

This project studies the interaction of:

> semantic similarity × collateral damage × reversibility × aggregate-metric masking

The goal is not merely to show that retain-forget entanglement exists, but to test whether **similarity-stratified evaluation reveals localized failures and recovery behavior that aggregate metrics hide**.

## Hypotheses

- **H1 — Collateral damage:** retain samples closer to the forget set in representation space suffer larger utility degradation after unlearning.
- **H2 — Reversibility:** forgotten behavior is more recoverable in high-similarity regions.
- **H3 — Aggregate masking:** dataset-level metrics can hide subgroup failures concentrated in high-similarity regions.

## Pilot

- **Dataset:** CIFAR-100
- **Model:** ResNet18
- **Forget ratio:** 1%, 5% first; 10% as expansion
- **Representation:** original model penultimate features
- **Similarity:** cosine similarity between retain and forget representations
- **Bins:** low / mid / high similarity
- **Core baselines:** exact retraining, retain-only fine-tuning, negative-gradient family, plus 1–2 representative unlearning methods

### Primary subgroup metric

For similarity bin (k):

[
\Delta U_k =
\mathrm{Acc}_{before}(retain,k)
-
\mathrm{Acc}_{after}(retain,k)
]

Additional evaluation:

- forget utility
- membership-inference AUC
- distance to exact retraining
- representation drift
- recovery of forgotten behavior after controlled relearning

## Minimum decisive experiment

Start small:

- 1 dataset
- 1 model
- 1–2 forget ratios
- 2–3 unlearning methods
- similarity-stratified retain evaluation
- controlled relearning experiment

Decision rule:

- **GO:** high-similarity retain samples show consistently larger collateral damage and/or stronger recovery.
- **CONDITIONAL GO:** static representation similarity is weak, but gradient similarity is informative → pivot toward gradient geometry.
- **KILL:** no meaningful stratification is reproducible under any reasonable similarity definition.

## Repository layout

```text
.
├── configs/                 # experiment configuration
├── docs/                    # research plan, protocol, literature notes
├── references/              # paper / literature tracking
├── results/                 # tracked summaries, figures, tables
├── scripts/                 # executable experiment entry points
├── src/                     # reusable research code
├── .gitignore
└── README.md
```

Large datasets, checkpoints, raw experiment outputs, and local tracking artifacts are intentionally excluded from Git.

## Milestones

- **2026-09-28 ~ 2026-10-02:** professor proposal / PASS decision
- **by 2026-10-12:** secure main finding and main contribution figure
- **2026-11:** robustness and expanded experiments
- **by 2026-12-14:** finish experiments and thesis manuscript

See [docs/research_plan.md](docs/research_plan.md) and [docs/experiment_protocol.md](docs/experiment_protocol.md) for the working design.
