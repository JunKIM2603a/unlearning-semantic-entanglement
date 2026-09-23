# Experiment Protocol

## A. Base model

1. Train ResNet18 on CIFAR-100.
2. Save the original checkpoint.
3. Cache penultimate representations for train/test samples.
4. Record sample IDs, labels, and split membership so every later result is traceable.

## B. Forget / retain construction

For each forget ratio:

- sample forget set (F)
- define retain set (R = D_{train} \setminus F)
- save the exact sample IDs

Initial ratios:

- 0.01
- 0.05

Expand to 0.10 only after the pilot is stable.

Where possible, keep the forgetting protocol fixed across methods so method comparison is paired.

## C. Similarity stratification

Using the **original pre-unlearning model**:

1. extract penultimate feature (h(x))
2. L2-normalize features
3. compute forget-retain cosine similarity
4. derive one score per retain sample

Pilot score:

[
s(r,F)=\max_{f\in F}\cos(h(r),h(f))
]

Split (R) into equal-count low / mid / high bins using the score.

Important: save bin assignments before running unlearning. Do not redefine bins using the unlearned model.

## D. Unlearning conditions

Minimum:

1. exact retraining on retain set
2. retain-only fine-tuning
3. negative-gradient baseline

Add representative methods after the minimum pipeline runs end-to-end.

For each condition, log:

- random seed
- checkpoint hash / identifier
- optimizer and learning rate
- epochs / steps
- forget ratio
- forget IDs
- runtime
- GPU memory if useful

## E. Collateral-damage evaluation

Compute retain accuracy:

- overall
- low-similarity bin
- mid-similarity bin
- high-similarity bin

For each bin (k):

[
\Delta U_k =
\mathrm{Acc}_{before}(R_k)
-
\mathrm{Acc}_{after}(R_k)
]

Primary figure candidate:

- x-axis: similarity bin
- y-axis: retain accuracy drop
- separate line / marker group per unlearning method

Also inspect continuous similarity rather than relying only on bins:

- sample-level similarity vs error transition
- binned trend with confidence intervals

## F. Class-confounding checks

Semantic similarity can largely reproduce class identity. Record:

- fraction of nearest forget neighbors with same label
- bin label distributions
- per-class bin counts

At minimum, perform one class-controlled analysis:

- within-class quantile binning, or
- label-matched high vs low similarity comparison

Do not interpret a high-bin effect as semantic entanglement until this confound is checked.

## G. Reversibility protocol

Start from each unlearned checkpoint.

Apply a **fixed, identical relearning budget** using forgotten data and evaluate at predefined checkpoints.

Track:

- forget accuracy recovery
- retain accuracy during relearning
- recovery AUC
- distance toward the original model / away from exact retraining

The relearning optimizer, LR, batch size, and number of examples must be identical when comparing similarity conditions or methods.

Avoid choosing the stopping point after seeing which method recovers fastest.

## H. Aggregate masking analysis

For every run place these values side-by-side:

- aggregate retain degradation
- low-bin degradation
- mid-bin degradation
- high-bin degradation

Main question:

> Would the conclusion change if only the aggregate retain metric were reported?

This should be answered descriptively with uncertainty, not only by visual impression.

## I. Reproducibility

Pilot:

- seed 0 to validate the complete pipeline

After the pipeline is fixed:

- multiple independent seeds
- report mean and uncertainty
- preserve exact split IDs and configs

Do not spend the early schedule on large baseline sweeps before the minimum decisive experiment is working.
