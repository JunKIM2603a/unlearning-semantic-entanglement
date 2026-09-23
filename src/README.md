# Source layout

Recommended modules:

```text
src/
├── data/          # CIFAR-100 loading, sample IDs, forget/retain splits
├── models/        # ResNet18 construction and feature extraction
├── similarity/    # cosine / gradient similarity and stratification
├── unlearning/    # exact retraining and approximate methods
├── evaluation/    # utility, MIA, drift, model distance
└── relearning/    # controlled reversibility experiments
```

Key implementation rule: preserve stable sample IDs across every stage so similarity bins, unlearning outputs, and recovery measurements can be joined exactly.
