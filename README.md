# LLM-105 Allegro Potentials

[![Open the NVE demonstration in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dantasqu/llm105-allegro-potentials/blob/main/notebooks/LLM105_Allegro_NVE_Colab.ipynb)

This pre-publication repository contains the machine-learned interatomic-potential model files used in a study of multi-dataset Allegro models transferred and fine-tuned for LLM-105 (2,6-diamino-3,5-dinitropyrazine-1-oxide).

## Contents

| Directory | Files | Description |
| --- | ---: | --- |
| `models/base/` | 12 | Base models associated with the dataset/reference conditioning tag named in each file. |
| `models/fine_tuned/` | 12 | Corresponding models after fine-tuning on the LLM-105 PBE-D3 dataset. |
| `models/specialist/` | 5 | LLM-105 specialist models trained from scratch using five independent data partitions. |
| `models/MODEL_MANIFEST.csv` | 1 | Model identity, conditioning tag, training stage, source datasets, size, checksum, and original archive filename. |
| `models/SHA256SUMS` | 1 | SHA-256 checksums for every model file. |
| `examples/nve/` | 3 | Verified LAMMPS NVE input, 76-atom unit cell, and protocol notes; the input creates the 304-atom `2×1×2` supercell used in the study. |
| `notebooks/` | 1 | Google Colab reviewer demonstration that builds LAMMPS with Allegro and runs a shortened NVE check. |

All model files use the `.nequip.pth` format.

## Reviewer demonstration

Open `notebooks/LLM105_Allegro_NVE_Colab.ipynb` in Google Colab and select a GPU runtime. The notebook follows the official NequIP/Allegro LAMMPS installation procedure, builds the pinned historical LAMMPS interface with Kokkos/CUDA, downloads only the displayed model D / OMC25 fine-tuned checkpoint, verifies its checksum and embedded atom ordering, and runs a short NVE check on the 76-atom unit cell.

The Colab workflow was validated end to end on a free T4 GPU on 13 September 2026: LAMMPS reached 100% GPU utilization, used about 4.6 GiB of GPU memory, and exited successfully. A fresh compilation takes roughly 45–70 minutes on Colab's two CPU cores; the 20-step gentle start and 100-step production NVE calculation then take only seconds.

The original `examples/nve/in.nve` is preserved unchanged. It requests a `2×1×2` replication to 304 atoms, 5,000 gentle-start steps at 0.1 fs, and up to 10,000,000 production steps at 0.5 fs. That paper-scale protocol is intended for the validated multi-GPU HPC environment. The one-rank historical wrapper did not handle the replicated 304-atom case reliably in Colab, so the notebook openly uses the 76-atom cell as a reviewer smoke test while retaining the same model, atom mapping, velocity initialization, timesteps, and NVE integrator.

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
