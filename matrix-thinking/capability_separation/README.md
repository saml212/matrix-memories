# capability_separation: the rank-law experiments

Code behind *The Rank the Task Demands: A Causal Rank Law for Matrix Memories
Trained on Group Composition* (`papers/neurreps-ea/arxiv-v3/`). A small
Transformer encoder maps a word over a finite group's generators to a single
matrix state Z, trained by cosine loss toward the group's reference
representation. We measure the effective rank the state recruits and, in the
causal arm, truncate Z to a fixed rank during training.

## Files

| File | What it does |
|---|---|
| `groups.py` | The five groups (S3, S4, A5, S5, A6), their orthogonal reference representations, d_min, d_state = d_min + 2, and the zero- or identity-padded target |
| `group_task.py` | Word sampling (train L in 1..8), eval-word sampling, coverage guards |
| `group_word_encoder.py` | The encoder, the single-state bottleneck, the optional rank truncation (`force_rank_k`), the cosine loss |
| `readout.py` | The instrument: centered-covariance subspace, restricted effective rank, scale and Procrustes degauging, rec@0.9 (the `crosscheck_*` fields are the decisional readout for force-rank cells) |
| `force_rank_arms.py` | The per-group force-rank grid k in {d_min−1, d_min, d_min+1} |
| `run_capability_sep.py` | Runner: `--smoke`, `--calibration-only`, `--sweep` (observational), `--m3fix` (zero-padded causal razor; `--m3fix-seed`, `--m3fix-groups`, `--steps`) |
| `blank_out.py` | Gradient blank-out test that the decoder reads only Z |
| `tost_analysis.py`, `marquee_power_simulation.py`, `spearman_null_calibration.py` | The S4/A5 equivalence test, its power simulation, and the exact Spearman null |
| `gate1_synthetic_injection.py`, `verify_option_a_readout.py`, `coverage_calibration.py`, `truncation_curve.py`, `budget_guard.py` | Instrument checks and gates |
| `stage2_*.py`, `smoke_stage2.py`, `beta_fla_smoke.py` | Stage 2 (recurrent composer). Not part of the rank-law paper |

Rank truncation and the entropy effective rank live in
`../deltanet_rd/rank_utils.py` (`truncate_to_rank` projects Z onto its top-k
left singular subspace through an eigendecomposition of ZZᵀ; gradients flow
through the projection).

## Run

```bash
pip install -r ../../requirements.txt
python run_capability_sep.py --smoke                                   # CPU
export CAPABILITY_SEP_PI_SIGNOFF=1                                     # the runner refuses GPU cells without it
python run_capability_sep.py --calibration-only --device cuda
python run_capability_sep.py --sweep --device cuda                     # 58 cells, observational arm
python run_capability_sep.py --m3fix --m3fix-seed 0 --device cuda      # 30 cells, causal razor
python run_capability_sep.py --m3fix --m3fix-seed 1 --m3fix-groups S4,A5,S5,A6 --device cuda
python run_capability_sep.py --m3fix --m3fix-groups S5 --steps 20000 --m3fix-seed 0 --device cuda
```

Step pins: S3 8k, S4 20k, A5 20k, S5 8k (razor re-pinned to 20k), A6 40k.
Results are one JSON per cell in `--results-dir`.

## Archived results

The runs the paper reports, with md5 manifests:

- `experiment-runs/2026-07-09_capability_sweep_harvest/` — observational sweep (19 unconstrained cells used in the paper)
- `experiment-runs/2026-07-09_m3fix_harvest/` — causal razor, seed 0, all five groups
- `experiment-runs/2026-07-09_m3fix_s3ext/` — S3 seeds 1–3
- `experiment-runs/2026-09-03_m3fix_ext4/` — S4, A5, S5, A6 seeds 1–3
- `experiment-runs/2026-09-03_m3fix_s5_20k/` — S5 seeds 0–3 at the 20k pin

Pre-registrations and verdicts: `../CAPABILITY_SEPARATION_DESIGN.md` §1.33–§1.36c.
Paper-to-evidence map: `papers/neurreps-ea/arxiv-v3/README.md`.
