# Footprint model

Notebook 04 uses the two-dimensional Flux Footprint Prediction (FFP) model of Kljun et al. (2015).
Its Python implementation is distributed by the authors and is not included in this repository.

1. Download the Python version of the FFP climatology code from https://footprint.kljun.net
2. Save `calc_footprint_FFP_climatology.py` in this folder (`src/`).

Notebook 04 adds `../src` to the Python path and imports `FFP_climatology` from it.

Reference: Kljun, N., Calanca, P., Rotach, M. W., & Schmid, H. P. (2015). A simple two-dimensional
parameterisation for Flux Footprint Prediction (FFP). *Geoscientific Model Development*, 8, 3695-3713.
https://doi.org/10.5194/gmd-8-3695-2015
