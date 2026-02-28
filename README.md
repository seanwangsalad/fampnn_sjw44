# Full-atom MPNN — Sidechain Packing

Minimal sidechain packing script using [FAMPNN](https://www.biorxiv.org/content/10.1101/2025.02.13.637498v1). Given a PDB with a backbone and sequence, packs sidechains using the FAMPNN 0.3Å model.

# Installation

```bash
conda create -n fampnn python=3.10
conda activate fampnn
pip install torch  # see https://pytorch.org/get-started/locally/ for your CUDA version
pip install -e .
```

## Model weights

Place weights under `weights/`. The script defaults to `weights/fampnn_0_3.pt`.

| Model | Weights | Description |
| ----- | ------- | ----------- |
| FAMPNN (0.0Å) | `fampnn_0_0.pt` | Best for packing. |
| FAMPNN (0.3Å) | `fampnn_0_3.pt` | Recommended for sequence design. **(default)** |
| FAMPNN (0.3Å, CATH) | `fampnn_0_3_cath.pt` | Best for mutation scoring. |

# Usage

```bash
python pack_sidechains.py input.pdb output.pdb [weights/fampnn_0_3.pt]
```

- `input.pdb` — PDB with backbone + sequence (sidechain atoms are ignored)
- `output.pdb` — packed full-atom structure; per-atom confidence (PSCE) is stored in the B-factor column
- checkpoint is optional; defaults to `weights/fampnn_0_3.pt`

Or call it from Python:

```python
from pack_sidechains import pack_sidechains
pack_sidechains("input.pdb", "output.pdb")
```
