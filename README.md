# matrix-memories

Matrix-valued state as a representational medium for language models. The
question running through everything here: when a task fixes how many
independent directions a representation needs, does gradient descent recruit
exactly that many, and can you measure it without fooling yourself?

Samuel Larson, Pebble ML (samlarson@pebbleml.com). Readable research notes
for every result live at [pebbleml.com](https://pebbleml.com).

## Papers

| Paper | Status | Read | Code | Evidence |
|---|---|---|---|---|
| **The Gradient Does Not See Rank: Rank-Indifference in Matrix-CODI on ProsQA** | ICML 2026 Mechanistic Interpretability Workshop (accepted). arXiv:2609.03090 | [arXiv](https://arxiv.org/abs/2609.03090) · [OpenReview](https://openreview.net/forum?id=Spof4PusVI) · [LaTeX source](matrix-thinking/submissions/icml-mi-workshop-2026/) · [finding page](https://pebbleml.com/findings/matrix-codi-rank-blindness.html) | [saml212/matrix-codi-rank-blindness](https://github.com/saml212/matrix-codi-rank-blindness) (MIT) | rank-eval JSONs in the code repo; run archives in `experiment-runs/2026-04-*` |
| **When the Gradient Sees Rank: Provable Necessity, Causal Recruitment, and Composition in Trained Matrix Memories** | arXiv, submitted September 2026 (ID pending) | [PDF](papers/rank-recruitment-ws/arxiv-v3/main.pdf) · [LaTeX source](papers/rank-recruitment-ws/arxiv-v3/) | [matrix-thinking/chapter2/](matrix-thinking/chapter2/) (`run_task_d.py` binding, `run_task_e.py` composition, `analyze_zdump.py` entity subspace) | evidence rows in [papers/rank-recruitment-ws/brief.md](papers/rank-recruitment-ws/brief.md); archives `experiment-runs/2026-07-01_task_e_20k`, `2026-07-02_task_e_*`, `2026-07-02_stage0_waves` |
| **The Rank the Task Demands: A Causal Rank Law for Matrix Memories Trained on Group Composition** | arXiv, submitted September 2026 (ID pending) | [PDF](papers/neurreps-ea/arxiv-v3/main.pdf) · [LaTeX source](papers/neurreps-ea/arxiv-v3/) · [finding page](https://pebbleml.com/findings/rank-law.html) | [matrix-thinking/capability_separation/](matrix-thinking/capability_separation/) | [paper-to-evidence map](papers/neurreps-ea/arxiv-v3/README.md); every number traces to a JSON in `experiment-runs/` |

The second and third papers are companions: the binding paper establishes the
rank law on K-pair associative memory, the rank-law paper extends it to group
composition. Each cites the other by title until both arXiv IDs exist.

The arXiv version of the ICML paper corrects one data-entry error in the
workshop version (the seed-1337 replication accuracy; three-seed mean
81.0 ± 2.0pp, was 81.5 ± 1.2pp). The full audit trail is in
[CORRECTION_2026-09-01.md](matrix-thinking/submissions/icml-mi-workshop-2026/CORRECTION_2026-09-01.md).

Further papers (associative binding, constant-memory recall, capacity) are in
preparation under [papers/](papers/).

## Reproduce

Python 3.10+, `pip install -r requirements.txt`. Both papers' experiments
run on a single GPU; smoke tests run on CPU.

**ICML paper.** Follow the README in
[saml212/matrix-codi-rank-blindness](https://github.com/saml212/matrix-codi-rank-blindness):
a CPU smoke test, then one `torchrun` command per training run.

**Rank law.** From the repo root:

```bash
cd matrix-thinking/capability_separation
python run_capability_sep.py --smoke                                   # CPU, minutes
export CAPABILITY_SEP_PI_SIGNOFF=1                                     # required before any GPU cell
python run_capability_sep.py --calibration-only --device cuda          # pins per-group step budgets
python run_capability_sep.py --sweep --device cuda                     # observational sweep (Tables 3, 4)
python run_capability_sep.py --m3fix --m3fix-seed 0 --device cuda      # causal razor, seed 0 (Table 1)
python run_capability_sep.py --m3fix --m3fix-seed 1 --m3fix-groups S4,A5,S5,A6 --device cuda   # seeds 1-3 likewise
python run_capability_sep.py --m3fix --m3fix-groups S5 --steps 20000 --m3fix-seed 0 --device cuda  # S5 20k re-test
```

The whole rank-law program is under 10 GPU-hours on an H100. Regenerate the
paper's figures from the archived, md5-checked JSONs with
`python papers/neurreps-ea/figures/figure_gen_arxiv_v3.py --out papers/neurreps-ea/arxiv-v3/figures`.

## Repository map

- `papers/` — paper sources, one directory per paper. `papers/neurreps-ea/arxiv-v3/` is the submitted rank-law build.
- `matrix-thinking/` — model and experiment code. `capability_separation/` is the rank-law program; `deltanet_rd/` is the fast-weight (DeltaNet) program; `submissions/icml-mi-workshop-2026/` is the ICML paper source.
- `experiment-runs/` — the archived script and result JSONs for every run, dated. Files up to 25 MB are in git; larger payloads are on Hugging Face or offline (see `experiment-runs/README.md`).
- `EXPERIMENT_LOG.md` — chronological log of every experiment, with numbers.
- `STATE.md`, `matrix-thinking/*_DESIGN.md` — internal working state and pre-registration records. Dense; written for continuity between sessions, not as an introduction.
- `pebble-ai-site/` — source of pebbleml.com (deploys on push).
- `research/`, `archive/` — literature memos and closed directions.

## Artifacts on Hugging Face

- [Slamin/ncr-scaling-artifacts](https://huggingface.co/datasets/Slamin/ncr-scaling-artifacts) — checkpoints and results from the scaling program behind the forthcoming recall paper (3.9 TB). Layout mirrors the training box's paths (`ephemeral/`, `home/nvidia/`).

## How this repository is produced

Experiments are designed, run, audited, and logged by an AI research agent
under Sam Larson's direction. Every claim in a paper is checked against the
raw archive before it ships; the design records keep pre-registrations and
verdicts, including the negative and inconclusive ones.

## Citing

See [CITATION.cff](CITATION.cff).
