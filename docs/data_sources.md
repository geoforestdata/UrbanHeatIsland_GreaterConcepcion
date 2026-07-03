# Data Sources

## Landsat 8 Collection 2 Level 2

The notebook uses the Google Earth Engine image collection `LANDSAT/LC08/C02/T1_L2`. This product provides atmospherically corrected surface reflectance bands and land surface temperature bands suitable for regional remote sensing analysis.

The workflow uses summer scenes from:

- 2015-01-01 to 2015-03-31
- 2026-01-01 to 2026-03-31

## Google Earth Engine

Google Earth Engine is used to query Landsat scenes, apply cloud masking, build seasonal composites, calculate spectral indices, calculate SUHI layers, and export GeoTIFF outputs.

Users must authenticate with an Earth Engine account before running the analysis.

## IDE Chile DPA 2023

The study-area shapefile is derived from IDE Chile DPA 2023 administrative boundaries. The derived file represents the Greater Concepcion study area used in this workflow.

Included municipalities:

- Concepción
- Talcahuano
- Hualpén
- San Pedro de la Paz

## Derived Boundary File

The repository includes:

```text
data/admin_boundaries/GreaterConcepcion.shp
```

with its required companion files:

```text
GreaterConcepcion.dbf
GreaterConcepcion.shx
GreaterConcepcion.prj
GreaterConcepcion.cpg
```

The shapefile should remain in this relative path so the notebook can run in Colab and locally without absolute paths.

## Landsat Scale Factors

The notebook applies Landsat Collection 2 Level 2 scale factors:

- Surface reflectance: `SR * 0.0000275 - 0.2`
- Surface temperature: `ST_B10 * 0.00341802 + 149.0`

The surface temperature result is converted from Kelvin to degrees Celsius.

## LST and SUHI Interpretation

LST is land surface temperature, not near-surface air temperature. SUHI is calculated as each urban LST pixel minus a mean rural reference LST for the same summer period.

Positive Delta SUHI values indicate increased relative urban heat island intensity from 2015 to 2026. Negative values indicate decreased relative intensity.

Results depend on cloud masking, the definition of urban and rural reference pixels, spectral thresholds, Landsat 30 m resolution, coastal influence, and the selected summer period.
