# LLM-105 NVE example

This directory preserves the input files used for the LLM-105 stability protocol:

- `llm105_uc_std.data` is the 76-atom unit cell.
- `in.nve` replicates it `2×1×2` to 304 atoms, relaxes the atoms and cell, initializes velocities at 300 K, performs a 0.5 ps gentle start at a 0.1 fs timestep, and then begins NVE production at a 0.5 fs timestep.

The archived input is intentionally unchanged. Its final `run 10000000` command is a production-scale calculation, and its `pair_coeff` line records the original HPC checkpoint path. It is intended for the validated multi-GPU HPC environment.

For a portable reviewer check, use [`notebooks/LLM105_Allegro_NVE_Colab.ipynb`](../../notebooks/LLM105_Allegro_NVE_Colab.ipynb). The notebook verifies the selected model and inputs, downloads a checksummed T4 build of the historical Kokkos/CUDA interface (with a pinned source-build fallback), and runs the same NVE stages on the 76-atom unit cell. With the resources available in Colab, this is intended as a reviewer smoke test; the paper-scale trajectory remains an HPC calculation.

The atom-type order required by the supplied models is `C H N O`.
