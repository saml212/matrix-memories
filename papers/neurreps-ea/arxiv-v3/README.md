# The Rank the Task Demands: A Causal Rank Law for Matrix Memories Trained on Group Composition

Samuel Larson, Pebble ML. arXiv preprint, submitted September 2026 (ID pending).
This directory is the submitted build: `main.pdf` (11 pages) and its source.

## Build

```bash
tectonic --keep-intermediates main.tex   # run three times from a clean tree
```

`main.bbl` is committed because arXiv does not run BibTeX. Upload
`main.tex`, `sections/`, `figures/`, `refs.bib`, `main.bbl`, and `neurips.sty`.

## Figures

Both figures are generated from the archived JSONs, whose md5s are pinned
in the generator:

```bash
python papers/neurreps-ea/figures/figure_gen_arxiv_v3.py --out papers/neurreps-ea/arxiv-v3/figures
```

## Where every number comes from

Code: [`matrix-thinking/capability_separation/`](../../../matrix-thinking/capability_separation/README.md).
Design record with the pre-registrations: `matrix-thinking/CAPABILITY_SEPARATION_DESIGN.md`
(§1.33 sweep harvest, §1.36 razor harvest, §1.36a S3 seeds, §1.36b four-group seeds, §1.36c S5 20k re-test).

| Paper location | Claim | Archive (relative to repo root) |
|---|---|---|
| §3, Table 3, Fig. 1 | Restricted effective rank per seed; Spearman ρ = 0.9747; 19/19 in band | `experiment-runs/2026-07-09_capability_sweep_harvest/results/*__unconstrained__seed*.json` (19 files), `harvest_summary.json` |
| §4 | S4 vs A5 Welch TOST: diff +0.019, se 0.037, df 7.8, t = 13.06 / 14.12 | same `harvest_summary.json` (marquee block); the 10 S4/A5 JSONs |
| §5, Table 1, Fig. 2 (seed 0) | Razor cells at k = d_min−1, d_min, d_min+1 and anchors, zero-padded target | `experiment-runs/2026-07-09_m3fix_harvest/zero_pad__*.json` (20 files) |
| App. E (S3 seeds 1–3) | S3 four-seed razor detail; seed-mean 0.5625 vs fixed bar 0.495 | `experiment-runs/2026-07-09_m3fix_s3ext/zero_pad__S3__*.json` |
| App. F (S4, A5, A6 seeds 1–3) | Four-seed razor detail; seed-means 0.6875 / 0.6500 / 0.6750 | `experiment-runs/2026-09-03_m3fix_ext4/results/zero_pad__*.json`, `EXT4_VERDICT.json` |
| App. F (S5, 20k pin) | S5 four-seed re-test; seed-mean 0.7000 vs bar 0.6075; gate1a 0.959–0.981 | `experiment-runs/2026-09-03_m3fix_s5_20k/results/zero_pad__S5__*.json`, `S5_20K_VERDICT.json` |
| App. F caption (S5 8k disclosure) | S5 at 8k: four-seed mean 0.4125 vs fixed bar 0.450, all cells fail gate1a | `experiment-runs/2026-09-03_m3fix_ext4/results/zero_pad__S5__*.json` (8k), `harvest_analysis_output.txt` |
| Tables 4, 5 | Whole-matrix effective rank of anchors and razor cells | `whole_matrix_effective_rank` field in the files above |
| App. D, ceiling fractions | Below-d_min cosines as a fraction of √((d_min−1)/d_min) | `crosscheck_mean_cos` in the seed-0 `k_dmin_minus_1` files (S5 from the 20k directory) |
| App. D, centering | Uncentered lens 0.705 vs centered 0.9996 on a synthetic model | `experiment-runs/2026-07-09_capability_calib_recheck/gate1b_recheck.txt` |
| App. D, estimator dependence | Restricted stable rank 1.451 / 2.156 / 2.078 / 2.362 / 3.340 | `restricted_stable_rank` field in the 19 sweep JSONs |
| Table 8 | gate1a values at the 8k pins | `gate1a.min_val` in the seed-0 S3 and S5 (8k) files |

Each results JSON holds one cell: `crosscheck_recovered_frac_90` is the
decisional rec@0.9 (fitted-Q Procrustes readout), `crosscheck_mean_cos` the
mean cosine, `restricted_effective_rank` the lens-restricted entropy rank,
`whole_matrix_effective_rank` the full-state rank, `gate1a` the convergence
check, and `steps_completed` the step pin. Evaluation is 50 fresh words per
cell, 30 to fit the gauge and 20 scored, so rec@0.9 moves in steps of 0.05.

## Verification history

- 2026-09-02: defense brief and independent recomputation of the headline numbers from the raw JSONs (`../DEFENSE_BRIEF_2026-09-02.md`, `../brief.md` rows N1–N19).
- 2026-09-03: GPT scrub of the prose merged (`../SCRUB_LOG.md`).
- 2026-09-10: full re-check of v3 against the archive and the code before submission; every table cell matched. Corrections applied: the S5 8k sufficiency shortfall disclosed in App. F, the S4 inversion count, ceiling fractions at the 20k S5 pin, Table 8 caption scope, the eval-set size in §2.
