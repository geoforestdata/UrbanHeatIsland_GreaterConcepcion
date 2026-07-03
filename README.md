# Mapping Surface Urban Heat Island Change in Greater Concepción, Chile (2015-2026)

This repository contains a reproducible Google Earth Engine and Python workflow for mapping Surface Urban Heat Island (SUHI) change in Greater Concepción, Chile, between summer 2015 and summer 2026.

The analysis uses Landsat 8 Collection 2 Level 2 imagery, land surface temperature (LST), NDVI, MNDWI, NDBI, a spectral-index urban mask, and a spectral-index rural reference mask. It is designed to run in Google Colab or in a local Python environment.


[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/geoforestdata/UrbanHeatIsland_GreaterConcepcion/blob/main/UrbanHeatIsland_GreaterConcepcion.ipynb)

## Study Area

The study area covers four municipalities in Greater Concepción:

- Concepción
- Talcahuano
- Hualpén
- San Pedro de la Paz

The boundary file `data/admin_boundaries/GreaterConcepcion.shp` is derived from the IDE Chile DPA 2023 administrative boundary dataset and clipped or dissolved to the four Greater Concepción municipalities listed above.

## Data Sources

- Landsat 8 Collection 2 Level 2 imagery from Google Earth Engine
- Landsat QA_PIXEL quality assessment band for cloud and shadow masking
- IDE Chile DPA 2023 administrative boundaries
- Derived local boundary: `data/admin_boundaries/GreaterConcepcion.shp`

## Method Overview

1. Load the official Greater Concepcion study-area boundary.
2. Build summer Landsat 8 composites for January-March 2015 and January-March 2026.
3. Apply Landsat Collection 2 Level 2 scale factors.
4. Calculate LST in degrees Celsius.
5. Calculate NDVI, MNDWI, and NDBI.
6. Build an urban mask using spectral-index thresholds that exclude water, dense vegetation, and non-urban surfaces.
7. Build a rural reference mask using vegetated, non-water, non-built-up pixels.
8. Calculate SUHI for each year as urban LST minus mean rural LST.
9. Calculate Delta SUHI as SUHI 2026 minus SUHI 2015.
10. Export GeoTIFFs, figures, and summary statistics.

## Repository Structure

```text
UrbanHeatIsland_GreaterConcepcion/
├── README.md
├── UrbanHeatIsland_GreaterConcepcion.ipynb
├── requirements.txt
├── .gitignore
├── LICENSE
├── data/
│   └── admin_boundaries/
│       ├── GreaterConcepcion.shp
│       ├── GreaterConcepcion.dbf
│       ├── GreaterConcepcion.shx
│       ├── GreaterConcepcion.prj
│       └── GreaterConcepcion.cpg
├── outputs/
│   ├── figures/
│   ├── geotiffs/
│   └── tables/
└── docs/
    └── data_sources.md
```

## Run in Google Colab

1. Upload or clone this repository into the Colab runtime.
2. Open `UrbanHeatIsland_GreaterConcepcion.ipynb`.
3. Run the notebook from top to bottom.
4. Authenticate Google Earth Engine when prompted.
5. Confirm that the shapefile and its companion files are present in `data/admin_boundaries/`.

The first notebook section installs missing Python packages only when the notebook is running in Colab.

## Run Locally

Create and activate a Python environment, then install the required packages:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Then start Jupyter and run the notebook:

```bash
jupyter lab
```

You must have access to Google Earth Engine and authenticate when prompted.

## Expected Outputs

The notebook writes outputs to:

- `outputs/geotiffs/LST_2015.tif`
- `outputs/geotiffs/LST_2026.tif`
- `outputs/geotiffs/Delta_LST.tif`
- `outputs/geotiffs/SUHI_2015.tif`
- `outputs/geotiffs/SUHI_2026.tif`
- `outputs/geotiffs/Delta_SUHI.tif`
- `outputs/tables/summary_statistics.csv`
- `outputs/figures/Figure_01_Study_Area.png`
- `outputs/figures/Figure_02_LST_2015.png`
- `outputs/figures/Figure_03_LST_2026.png`
- `outputs/figures/Figure_04_Delta_LST.png`
- `outputs/figures/Figure_05_SUHI_2015.png`
- `outputs/figures/Figure_06_SUHI_2026.png`
- `outputs/figures/Figure_07_Delta_SUHI.png`
- `outputs/figures/Figure_08_Comparison_LST_SUHI.png`

## Limitations

This is a demonstration workflow, not an operational climate-risk product. Landsat LST is land surface temperature, not air temperature. SUHI values are relative to the rural reference selected in this workflow.

Results depend on cloud masking, summer date selection, spectral threshold choices, the rural reference definition, Landsat 30 m spatial resolution, and coastal influence in Greater Concepcion.

## Citation and Attribution

Please cite Google Earth Engine, the USGS Landsat 8 Collection 2 Level 2 product, and IDE Chile DPA 2023 when using or adapting this workflow. Also cite or acknowledge any derived figures, tables, or boundary files generated from this repository.
