# CR-ΛCDM — A CPT-Reheated ΛCDM Extension to Resolve the CMB Low-ℓ Deficit

**Author:** Christophe Bellat  
**Affiliations:** Independent researcher (Paris–Athens)  
**Contact:** christophe.bellat@proton.me  
**Preprint:** Zenodo DOI 10.5281/zenodo.17469405  
**License:** MIT (for scripts and configuration files)
---

## Overview

This repository provides a complete computational suite to reproduce and extend the results of the preprint:

> Bellat, C. (2025). *CR-ΛCDM: A CPT-Reheated ΛCDM Extension to Resolve the CMB Low-ℓ Deficit.* Zenodo. [doi:10.5281/zenodo.17469405](https://doi.org/10.5281/zenodo.17469405)

The **CR-ΛCDM** model introduces a minimal phenomenological extension of ΛCDM featuring a **CPT-symmetric reheating phase** that naturally generates an **infrared cutoff** in the primordial curvature power spectrum, offering a potential explanation for the observed low-ℓ deficit in the Planck 2018 CMB angular spectra.

---

## Repository structure

| Directory / File                    | Description                                               |
| ----------------------------------- | --------------------------------------------------------- |
| `cobaya_crlcdm_externalPk.yaml`     | CR-ΛCDM MCMC configuration (external primordial spectrum) |
| `cobaya_lcdm_baseline.yaml`         | Standard ΛCDM baseline configuration                      |
| `make_pr_from_params.py`            | Generate a single primordial spectrum CSV                 |
| `generate_pr_grid.py`               | Build a grid of primordial spectra over (kc, p)           |
| `batch_run_crlcdm_grid.sh`          | Sequential batch run of Cobaya over the grid              |
| `run_crlcdm_mpi.sh`                 | Parallel (10-job) execution for Apple Silicon or Linux    |
| `harvest_cobaya_results.py`         | Aggregate χ² results from Cobaya logs                     |
| `plot_crlcdm_heatmap.py`            | Generate the Δχ²(kc, p) heatmap (scientific style)        |
| `summarize_results.py`              | Print Δχ²\_min and corresponding (kc, p)                  |
| `orchestrate_crlcdm.sh`             | Full pipeline orchestration (grid + plot + archive)       |
| `README_CR-LCDM_MCMC_quickstart.md` | Minimal MCMC usage guide                                  |
| `install_crlcdm_env_mac.sh`         | Environment setup for macOS (Apple Silicon)               |

---

## Installation (macOS / Linux)

```bash
git clone https://github.com/<your_repo>/CR-LCDM.git
cd CR-LCDM
chmod +x install_crlcdm_env_mac.sh
./install_crlcdm_env_mac.sh
```

Ensure the **Planck 2018 likelihoods (clik\_18.11)** are downloaded from the ESA Planck Legacy Archive  
and placed in `~/Downloads/clik_18.11.tar.gz` before running the installer.

---

## Execution (Full Pipeline)

After installation:

```bash
cd ~/CR_LCDM
chmod +x orchestrate_crlcdm.sh run_crlcdm_mpi.sh
./orchestrate_crlcdm.sh
```

This script will:
1. Run the ΛCDM baseline,
2. Generate the (kc, p) grid,
3. Launch all CR-ΛCDM runs in parallel (10 cores),
4. Aggregate results (`results.csv`),
5. Plot Δχ²(kc, p) as `heatmap_dchi2.png` and `heatmap_dchi2.pdf`,
6. Archive everything under `CR_LCDM_RESULTS_YYYYMMDD_HHMMSS/`.

---

## Example output

- `results.csv` — table of (kc, p, χ²) values
- `heatmap_dchi2.png` — interpolated Δχ²(kc,p) relative to ΛCDM
- `SUMMARY.txt` — best-fit Δχ², kc, and p
- `CR_LCDM_RESULTS_*/` — archived results (chains, logs, plots)

---

## Requirements

- macOS (Apple Silicon) or Linux x86\_64
- Python ≥ 3.10
- [Cobaya](https://cobaya.readthedocs.io) ≥ 3.5
- [CLASS](https://lesgourg.github.io/class_public/) ≥ 3.2
- Planck 2018 likelihoods (plik TTTEEE, low-ℓ TT/EE, lensing)

---

## Citation

If you use this code or reproduce the results, please cite:

> **Bellat, C. (2025)**. *CR-ΛCDM: A CPT-Reheated ΛCDM Extension to Resolve the CMB Low-ℓ Deficit.*  
> Zenodo. DOI: [10.5281/zenodo.17469405](https://doi.org/10.5281/zenodo.17469405)

BibTeX:
```bibtex
@misc{bellat2025crlcdm,
  author       = {Bellat, Christophe},
  title        = {CR-ΛCDM: A CPT-Reheated ΛCDM Extension to Resolve the CMB Low-ℓ Deficit},
  year         = {2025},
  doi          = {10.5281/zenodo.17469405},
  url          = {https://doi.org/10.5281/zenodo.17469405}
}
```

---

## Acknowledgments

This research uses publicly available data from the **Planck 2018** CMB likelihoods  
and the **CLASS Boltzmann solver**.  
The Cobaya framework by Torrado & Lewis was used for Bayesian inference and MCMC sampling.

---

## Disclaimer

This repository is provided for scientific reproducibility and educational purposes.  
It is not affiliated with the Planck Collaboration.  
All original scripts © 2025 Christophe Bellat (MIT License).
