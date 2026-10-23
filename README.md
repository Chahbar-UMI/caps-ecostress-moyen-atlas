# caps-ecostress-moyen-atlas

[![Data DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23472840.svg)](https://doi.org/10.5281/zenodo.23472840)

This repository contains a processing chain that detects **cold-air pools** in the closed
depressions of the Central Middle Atlas (Morocco). It works from **ECOSTRESS** nocturnal
land surface temperature (LST, 70 m) combined with terrain morphology. The study area
covers 3,291 km², centred on three forests, over the period 2019–2026.

The pipeline is a single Google Colab / Jupyter notebook, `CAPS_ECOSTRESS_pipeline.ipynb`
(comments and outputs in French). In short, it:

1. builds (or extends) a multi-year cube of ECOSTRESS passes — L2T LSTE v002 with a MODIS
   MOD10A1F snow flag, stored as CF-1.8 NetCDF;
2. places each pass within the solar night (elapsed fraction, NOAA solar algorithm) and
   computes LST climatologies together with a local anomaly (pixel minus a 5 km background);
3. maps closed depressions by morphological reconstruction of the FABDEM DEM, and routes
   potential cold-air flow with a D8 algorithm that leaves the depressions unfilled;
4. fits, for each depression, a model of the floor − rim temperature difference against
   night fraction and season (bootstrap confidence intervals), then tests determinants,
   robustness and between-period stability. Example maps and series for publication are
   produced on request (`FIGURES_EXEMPLES`).

## Quick start

Open the notebook in Colab (*File → Open notebook → GitHub*) and run the cells in order.
Section 1 (configuration) is the only cell to edit.

| Mode | For | Data | Accounts |
|---|---|---|---|
| `autonome` (default) | anyone | data package downloaded automatically from Zenodo | none (NASA Earthdata only to rebuild the cube) |
| `auteur` | the author | author's Google Drive | Google Drive, NASA Earthdata, Google Earth Engine |

A standard CPU runtime is sufficient (RAM < 4 GB). Outputs are written to `sorties/` and `sorties/figures/`.
The Earthdata password is never stored in the notebook; it is requested interactively.

## Data availability

Input data package (ECOSTRESS cube, study-area boundary, snow cache, DEM- and land-cover-derived layers):
Chahbar, K. & Nejjari, A. (2026). *ECOSTRESS nocturnal land surface temperature data cube and cold-air pool
outputs, Central Middle Atlas (Morocco), 2019–2026*. Zenodo. https://doi.org/10.5281/zenodo.23472840

Source products: ECOSTRESS ECO_L2T_LSTE v002 (NASA LP DAAC), MOD10A1F v061 (NASA NSIDC DAAC),
FABDEM V1-0 (Hawker et al., 2022), ESA WorldCover 2021 v200 (Zanaga et al., 2022).

## Licences

- **Code**: MIT (see `LICENSE`).
- **Data package**: CC BY-NC-SA 4.0, because it contains layers derived from FABDEM (non-commercial, share-alike).
  ESA WorldCover is CC BY 4.0; ECOSTRESS and MODIS products are openly available from NASA.
- **Background imagery** in the example figures: Esri World Imagery (Esri Master License Agreement); credits are shown on each map, as Esri requires for publications.

## Citation

Please cite the software (see `CITATION.cff`, or *Cite this repository* on GitHub) and the data package.
Method and software references are in `references.bib` and in the last cell of the notebook.

## Contact

Kamal Chahbar — Université Moulay Ismail, Laboratoire LGEE — ORCID [0009-0008-3765-2316](https://orcid.org/0009-0008-3765-2316)
