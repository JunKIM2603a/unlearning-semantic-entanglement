# Professor Proposal Outline

Target: 2026-09-28 ~ 2026-10-02

## One-sentence question

Does semantic proximity to forgotten data identify retain subgroups that suffer disproportionate collateral damage and exhibit stronger reversibility after machine unlearning?

## Why this matters

Machine-unlearning results are often summarized by aggregate forget and retain metrics. Such averages may hide localized failure when forget and retain examples occupy nearby regions of representation space.

## What is already known

Retain-forget entanglement itself is not enough for novelty. The proposal should therefore avoid claiming that simply protecting similar retain samples is the contribution.

## Gap tested here

The project jointly tests:

- similarity-conditioned retain damage,
- similarity-conditioned reversibility,
- and whether aggregate metrics mask these failures.

## Fast experiment

- CIFAR-100
- ResNet18
- 1% and 5% forget ratios
- original-model penultimate cosine similarity
- low / mid / high retain similarity bins
- exact retraining + 2 approximate unlearning methods
- controlled relearning

## Falsifiable outcomes

- **GO:** high-similarity subgroup consistently shows stronger damage and/or recovery.
- **CONDITIONAL GO:** static similarity is weak but gradient similarity explains the pattern.
- **KILL:** no similarity definition gives reproducible stratification.

## Main contribution if successful

A similarity-stratified evaluation protocol showing where aggregate unlearning metrics conceal localized collateral damage and reversibility.

## Useful result if the main hypothesis fails

Evidence that static representation similarity is not a sufficient explanatory variable for unlearning entanglement, motivating gradient geometry / optimization-trajectory analysis.
