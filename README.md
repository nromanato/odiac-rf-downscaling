# Mass-preserving Random Forest downscaling of ODIAC CO₂ emissions

Code accompanying:

> Romanato, N., Wang, M., Maragno, D. (2026). *Earth Observation Predictors of
> Sub-Kilometre Anthropogenic CO₂ Emissions are Shaped by City Morphology:
> Evidence from Shanghai and Milan.* Submitted to *Environmental Modelling & Software*.

The pipeline redistributes ODIAC 2023 (release 2024) fossil-fuel CO₂ emissions
from 1/120° (~1 km) to 1/480° (~250 m) using a ten-band Earth Observation
predictor stack, conserving the parent-cell emission total exactly. It is
applied comparatively to Shanghai Pudong and the Metropolitan City of Milan.

**Code:** https://github.com/nromanato/odiac-rf-downscaling
**Input data and output products:** https://doi.org/10.5281/zenodo.22707984

## Contents

| File | Description |
|---|---|
| `ODIAC_RF_downscaling_release.ipynb` | Full pipeline, one city per run |
| `requirements.txt` | Python dependencies for local execution |
| `LICENSE` | MIT licence covering the code |

## Running the notebook

1. Open the notebook in Google Colab (or a local Jupyter environment).
2. In cell **0.2**, set `CITY` to `"shanghai_pudong"` or `"milan"`. There is no
   default: the choice is mandatory.
3. Run every cell in order. Cell **0.4** lists the input files required for the
   selected city and accepts them through the Colab upload widget; no Google
   Drive mount is used.
4. The final cell compares the run against the values reported in the
   manuscript and writes `verification_<city>.csv`.
5. Repeat for the second city.

Supplying a previously exported predictor stack named
`gee_features_fine_<city>.tif` skips the Earth Engine steps, allowing the
pipeline to be reproduced without an Earth Engine account. Both stacks are
included in the Zenodo deposit.

## Input files

Downloadable from the Zenodo deposit:

- `ODIAC_2024_01..12_<Shanghai|Milano>.tif` — monthly ODIAC rasters, reference
  year 2023, release 2024
- `pudong_aoi.*` / `milano_aoi.*` — study-area polygons
- `shanghai_jiedao_adm8.*` / `milano_comuni_adm8.*` — administrative units

Each shapefile requires its `.shp`, `.shx`, `.dbf` and `.prj` components.

The remaining predictors — GHS-BUILT-S and GHS-POP (P2023A), ESA WorldCover
v200, Sentinel-5P TROPOMI NO₂, Sentinel-2 SR Harmonized and NASADEM — are
retrieved at runtime from the Google Earth Engine catalogue and are not
redistributed here.

## Licence and attribution

The components of this work carry different terms.

| Component | Licence | Attribution required |
|---|---|---|
| Code in this repository | MIT | — |
| Downscaled rasters, zonal statistics, bootstrap products | CC BY 4.0 | cite the Zenodo deposit |
| ODIAC monthly subsets | CC BY 4.0 | Oda & Maksyutov, see below |
| Administrative boundaries | ODbL 1.0 | © OpenStreetMap contributors |

The administrative boundaries are derived from OpenStreetMap and remain under
the Open Database License: any redistributed derivative of those layers must be
released under the same terms. This is why the deposit is not licensed CC BY 4.0
as a whole.

ODIAC is distributed by the Center for Global Environmental Research, NIES,
under CC BY 4.0 and must be cited as:

> Oda, T., Maksyutov, S. (2015). *ODIAC Fossil Fuel CO₂ Emissions Dataset*
> (ODIAC2024). Center for Global Environmental Research, National Institute for
> Environmental Studies. https://doi.org/10.17595/20170411.001

## How to cite

Cite the article for the method and the Zenodo deposit for the code and data:

> Romanato, N., Wang, M., Maragno, D. (2026). *Earth Observation Predictors of
> Sub-Kilometre Anthropogenic CO₂ Emissions are Shaped by City Morphology:
> Evidence from Shanghai and Milan.* https://doi.org/10.5281/zenodo.22707984
