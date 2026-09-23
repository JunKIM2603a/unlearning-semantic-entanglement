# Research Plan

## 1. Problem

Machine unlearning should remove the influence of designated forget samples while preserving retained knowledge. Existing aggregate evaluation can miss whether damage is concentrated among retain samples that are semantically close to the forget set.

This project therefore asks whether **retain-forget semantic proximity predicts both collateral damage and reversibility**.

## 2. Novelty target

The contribution must not stop at “similar retain samples are vulnerable.”

The intended contribution is the joint analysis of:

1. representation-space similarity,
2. similarity-conditioned collateral damage,
3. similarity-conditioned reversibility,
4. failure modes hidden by aggregate metrics.

## 3. Hypotheses

### H1 — Similarity-conditioned collateral damage

For retain sample (r), let (s(r,F)) denote its similarity to the forget set (F). Higher (s(r,F)) should be associated with larger post-unlearning utility degradation.

Primary statistic for bin (k):

[
\Delta U_k =
\mathrm{Acc}_{before}(R_k)
-
\mathrm{Acc}_{after}(R_k)
]

Expected pattern:

[
\Delta U_{high} > \Delta U_{mid} > \Delta U_{low}
]

This ordering is a hypothesis, not an assumption; confidence intervals and seed consistency must be reported.

### H2 — Similarity-conditioned reversibility

After unlearning, conduct a controlled relearning procedure on forgotten data. Test whether high-similarity regions recover forgotten behavior faster or more strongly than low-similarity regions.

Recommended outputs:

- recovery curve versus relearning steps
- recovery AUC
- steps needed to reach a preregistered recovery level
- comparison against exact retraining

### H3 — Aggregate metric masking

Compare overall retain degradation with the three similarity-bin degradations.

A key failure pattern is:

- small aggregate retain drop,
- but materially larger drop in the high-similarity subgroup.

The analysis should report both aggregate and subgroup views rather than replacing one with the other.

## 4. Pilot scope

### Dataset / model

- CIFAR-100
- ResNet18

### Forget ratios

Priority:

1. 1%
2. 5%
3. 10% only after the pilot pipeline is stable

### Unlearning methods

Minimum set:

- exact retraining
- retain-only fine-tuning
- negative-gradient family
- 1–2 representative published unlearning methods if implementation cost fits the schedule

Exact retraining is the reference, not merely another approximate method.

## 5. Similarity definition

Base representation:

- penultimate representation from the original trained model
- cosine similarity

Pilot per-retain score:

[
s(r,F)=\max_{f\in F}\cos(h(r),h(f))
]

Then split retain samples into low / mid / high quantile bins.

### Required robustness checks

Nearest-forget similarity can be confounded by class identity. Therefore record labels and add at least one of:

- within-class similarity stratification,
- label-matched analysis,
- same-class vs different-class comparison.

If static representation similarity is weak, test gradient similarity before abandoning the question.

## 6. Metrics

### Primary

- similarity-bin retain degradation (Delta U_k)

### Secondary

- overall retain accuracy
- forget-set utility
- membership-inference AUC
- parameter or output distance to exact retraining
- representation drift
- relearning recovery curve / AUC

## 7. Minimum decisive experiment

The first decisive experiment should avoid breadth.

Use:

- CIFAR-100
- ResNet18
- forget ratios 1% and 5%
- exact retraining + 2 approximate unlearning methods
- 3 similarity bins
- at least one controlled relearning schedule

Run one seed for pipeline validation, then multiple seeds only after the analysis is correct.

## 8. Decision criteria

### GO

Proceed when high-similarity regions show a reproducible increase in collateral damage and/or recovery relative to low-similarity regions across the key methods or forget ratios.

### CONDITIONAL GO

If representation cosine similarity is weak but gradient similarity produces stable stratification, pivot the thesis toward **gradient geometry as a better explanatory variable for unlearning entanglement**.

### KILL

Stop this direction if no reasonable similarity definition produces reproducible stratification and no interpretable recovery relationship emerges.

A null result may still be useful if it establishes that static semantic similarity is not a sufficient explanatory variable.

## 9. Timeline

### 2026-09-28 ~ 2026-10-02

- verify literature gap
- finalize hypothesis and falsification criteria
- prepare professor proposal
- smoke-test training / unlearning pipeline

### by 2026-10-12

- obtain main similarity-stratified figure
- establish whether H1/H2 have a usable signal
- determine GO / CONDITIONAL GO / KILL

### November

- additional seeds
- alternative similarity definitions
- forget-ratio robustness
- class-conditioned controls
- extra unlearning baselines

### by 2026-12-14

- complete final experiments
- freeze tables / figures
- finish thesis manuscript
