# Wilson-Cowan modelling of binocular rivalry

A 2026 Computational Neuroscience coursework project exploring how mutual inhibition and adaptation influence perceptual switching, using a simplified two-population Wilson-Cowan-style model and empirical virtual-reality behavioural data.

**Research question:** How do changes in model parameters affect perceptual switching dynamics, and under what conditions can the model reproduce behavioural patterns in binocular rivalry?

## Workflow

1. Load and combine participant files across two experiments and Motion/Static conditions.
2. Identify percept identity, timestamps and durations; derive missing durations from successive timestamps.
3. Retain stable percepts (codes 1 and 2), remove missing/non-positive durations and durations of 100 or more.
4. Summarise dominance durations and approximate switches at participant and condition levels; compare conditions using t-tests.
5. Simulate two competing neural populations with self-excitation, mutual inhibition, adaptation and Gaussian input noise using Euler integration.
6. Explore inhibition (0.5–2.5; nine values) and adaptation strength (0.5–4.0; ten values), plotting switching and dominance-duration measures.

**Tools:** Python, NumPy, pandas, SciPy and matplotlib.

## Files

- [Analysis notebook](notebooks/rivalry-analysis.ipynb)
- [Original coursework report](docs/report.md), transcribed with figures and without the assessment coversheet
- [Methods diagram](docs/methods-diagram.png)
- [Empirical data requirements](data/README.md)

![Methods diagram](docs/methods-diagram.png)

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

Open the notebook and use `notebooks/` as its working directory. It expects authorised data under `../data/Data/`; see the data README for the folder structure. Empirical datasets are not included. Dependency versions are not pinned because the original environment was not supplied.

## Reproducibility status

This repository preserves the supplied coursework analysis, with privacy cleanup and a relative data path. It is **not yet a fully reproducible end-to-end analysis**:

- The notebook calls `extract_percepts(E1, E2)` and `compute_model_measures(percepts, dt)`, but their definitions/imports are absent from the supplied file. They must be recovered before the switching analysis and parameter sweeps can run from a clean kernel.
- All code cells pass Python syntax checks. The self-contained sigmoid and simulation definitions were run independently of the empirical data: the baseline simulation produced two finite arrays of 3,000 samples. This check does not verify reported behavioural statistics, switching metrics or scientific conclusions.
- Notebook outputs are cleared. Original report figures and findings are historical coursework results, not results regenerated for this publication.

## Interpretation notes

The report describes empirical comparisons and exploratory model behaviour, and acknowledges that parameters were not quantitatively fitted to the empirical data. The original report and figures are preserved; these points require review before extending its conclusions:

- The plotted adaptation sweeps fluctuate and do not establish the consistently monotonic trend described in parts of the report. Repeated simulations with uncertainty estimates would be needed to assess parameter effects.
- Reported Motion/Static comparisons use independent-samples t-tests, although the report describes repeated conditions within participants. Check participant pairing before choosing the statistical design; pooling repeated participant observations across conditions also needs review.
- Empirical switch counts are approximated as retained episode counts minus one. This may differ from counting actual percept transitions, particularly after exclusions.
- The loader selects only the first sorted text file per participant folder. Confirm that practice and experimental files are selected correctly and that timestamp-derived durations do not cross trial boundaries.
- The final cells labelled as baseline results reuse variables overwritten by the parameter sweeps; they do not reliably refer to the baseline run.
- The report contains a significance-threshold typo (p = .052 alongside “.005”); no statistical results have been recomputed or silently corrected here.

## Data and references

The empirical analysis cites Han et al. (2024), *Binocular rivalry under naturalistic geometry: Evidence from worlds simulated in virtual reality*. DOI: [10.1093/pnasnexus/pgae054](https://doi.org/10.1093/pnasnexus/pgae054). The coursework report contains its original reference list, including work on competition, adaptation and noise in perceptual rivalry. Dataset redistribution rights are not asserted.

## Privacy cleanup

Student identifiers have been removed from filenames and notebook content. Notebook outputs, execution counts and nonessential metadata are cleared. The report's assessment coversheet and document metadata are omitted, and all published images have embedded metadata removed. The raw DOCX, empirical data and participant-level outputs are not published. Original source files remain unchanged.
