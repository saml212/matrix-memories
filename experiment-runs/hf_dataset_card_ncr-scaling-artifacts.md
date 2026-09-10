---
license: cc-by-4.0
pretty_name: NCR scaling artifacts (matrix-states)
tags:
  - checkpoints
  - research-artifacts
  - fast-weights
  - matrix-representations
---

<!-- Upload this file as README.md at the root of huggingface.co/datasets/Slamin/ncr-scaling-artifacts.
     The YAML header above also stops the dataset viewer from trying to parse the ledger files as a table. -->

# NCR scaling artifacts

Checkpoints and per-cell results from the scaling program behind the
matrix-states research line (Samuel Larson, Pebble ML): Native Composition
Reads and constant-memory recall in a fast-weight language model at 98M, 392M,
and 1.31B parameters. Roughly 3.9 TB, uploaded from the training box in
September 2026 so that every checkpoint referenced in the forthcoming papers is
public.

Paper sources, code, and the small result JSONs live in
https://github.com/saml212/matrix-states. Readable research notes:
https://pebbleml.com.

## Layout

Paths mirror the training box, so the top level is `ephemeral/` and `home/`.

| Path | Contents |
|---|---|
| `ephemeral/scaleaxis/{ckpts,results,attribution,v2prime}` | 98M and 392M scale-axis cells: checkpoints, scored results, attribution runs, and the v2' variant |
| `ephemeral/scaleaxis1b/{ckpts,results,attribution}` | 1.31B cells: checkpoints, results, attribution |
| `ephemeral/kscaling/{ckpts,results}` | K-axis (number of stored operators) sweep |
| `ephemeral/reseed_ckpts/` | Fresh-seed replication checkpoints |
| `home/nvidia/queue/` | The job queue records that produced the cells (hypothesis, command, output dir, validity check per job) |

Checkpoints are PyTorch state dicts; results are JSON, one per cell. The
matching analysis scripts and md5 manifests are in the GitHub repository under
`experiment-runs/2026-08-*` and `experiment-runs/2026-09-0*`.

## Citation

See `CITATION.cff` in https://github.com/saml212/matrix-states.
