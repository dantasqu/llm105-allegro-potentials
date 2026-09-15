# LLM-105 NVE example

This directory contains the input files for the LLM-105 NVE stability simulation:

- `llm105_uc_std.data` is the 76-atom unit cell.
- `in.nve` creates the 304-atom `2×1×2` supercell and runs the HPC NVE workflow.

For a portable GPU demonstration, **[open the NVE notebook in Google Colab](https://colab.research.google.com/github/dantasqu/llm105-allegro-potentials/blob/main/notebooks/LLM105_Allegro_NVE_Colab.ipynb)**. The notebook configures the files, verifies the installation, and runs the 76-atom NVE simulation on an NVIDIA T4.

The atom-type order required by the supplied models is `C H N O`.
