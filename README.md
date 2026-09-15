# LLM-105 Allegro Potentials

[![Open the NVE demonstration in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dantasqu/llm105-allegro-potentials/blob/main/notebooks/LLM105_Allegro_NVE_Colab.ipynb) [![Latest release](https://img.shields.io/github/v/release/dantasqu/llm105-allegro-potentials?label=release)](https://github.com/dantasqu/llm105-allegro-potentials/releases/latest)

This repository contains the machine-learned interatomic-potential model files used in a study of multi-dataset Allegro models transferred and fine-tuned for LLM-105 (2,6-diamino-3,5-dinitropyrazine-1-oxide).

**[Run the NVE demonstration in Google Colab](https://colab.research.google.com/github/dantasqu/llm105-allegro-potentials/blob/main/notebooks/LLM105_Allegro_NVE_Colab.ipynb)**

## Quick start

1. Click the **Open in Colab** badge above.
2. Select **Runtime → Change runtime type → T4 GPU**.
3. Select **Runtime → Run all**. No GitHub login or token is required.

The notebook downloads and verifies the T4 LAMMPS + Allegro executable and fine-tuned model D (OMC25), runs an NVE simulation on the 76-atom unit cell, and plots temperature and total energy. A successful run reports `Exit code: 0`. The 304-atom HPC input is available in `examples/nve/`.

## Release downloads

The **[latest release](https://github.com/dantasqu/llm105-allegro-potentials/releases/latest)** provides the Colab notebook, fine-tuned model D (OMC25), the 304-atom HPC NVE input, the 76-atom structure, and `DEMO_SHA256SUMS` as separate downloads. This allows the demonstration files to be downloaded without retrieving every model in the repository.

## Contents

| Directory | Files | Description |
| --- | ---: | --- |
| `models/base/` | 12 | Base models associated with the dataset/reference conditioning tag named in each file. |
| `models/fine_tuned/` | 12 | Corresponding models after fine-tuning on the LLM-105 PBE-D3 dataset. |
| `models/specialist/` | 5 | LLM-105 specialist models trained from scratch using five independent data partitions. |
| `models/MODEL_MANIFEST.csv` | 1 | Model identity, conditioning tag, training stage, source datasets, size, checksum, and original archive filename. |
| `models/SHA256SUMS` | 1 | SHA-256 checksums for every model file. |
| `examples/nve/` | 3 | Verified LAMMPS NVE input, 76-atom unit cell, and protocol notes; the input creates the 304-atom `2×1×2` supercell used in the study. |
| `notebooks/` | 1 | Google Colab demonstration that downloads a verified T4 executable and runs a shortened NVE simulation. |

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
