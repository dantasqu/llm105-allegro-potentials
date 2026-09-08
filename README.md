# LLM-105 Allegro Potentials

This pre-publication repository contains the machine-learned interatomic-potential model files used in a study of multi-dataset Allegro models transferred and fine-tuned for LLM-105 (2,6-diamino-3,5-dinitropyrazine-1-oxide).

## Contents

| Directory | Files | Description |
| --- | ---: | --- |
| `models/base/` | 12 | Base models associated with the dataset/reference conditioning tag named in each file. |
| `models/fine_tuned/` | 12 | Corresponding models after fine-tuning on the LLM-105 PBE-D3 dataset. |
| `models/specialist/` | 5 | LLM-105 specialist models trained from scratch using five independent data partitions. |
| `models/MODEL_MANIFEST.csv` | 1 | Model identity, conditioning tag, training stage, source datasets, size, checksum, and original archive filename. |
| `models/SHA256SUMS` | 1 | SHA-256 checksums for every model file. |

All model files use the `.nequip.pth` format.

## Model naming

The filename identifies the model family, displayed model identity, and conditioning tag:

```text
base_model_<a-d>_<mptrj|spice2|t1x|omc25>.nequip.pth
finetuned_model_<a-d>_<mptrj|spice2|t1x|omc25>_llm105.nequip.pth
llm105_specialist_fold_<1-5>.nequip.pth
```

The model identities follow the manuscript convention:

| Displayed model | Source datasets used in base training |
| --- | --- |
| A | MPtrj, SPICE2 |
| B | MPtrj, SPICE2, OMC25 |
| C | MPtrj, SPICE2, T1x |
| D | MPtrj, SPICE2, T1x, OMC25 |

Each base model was jointly trained on the source datasets listed above; it was not trained separately for each tag. The tag in each filename selects the dataset/reference condition used with that model. The `fine_tuned` models were fully fine-tuned on 42,096 LLM-105 configurations calculated with PBE-D3. The specialist models used the same LLM-105 data pool and architecture but were trained from scratch.
