# Data directory

The notebooks in this repository expect the following files in `data/`. They are
**not committed** to the repository because the dengue case counts are restricted
(see below). They are listed here so the expected schema is clear and the code can
be re-run once access is obtained.

## Expected files

| File | Description | Availability |
|------|-------------|--------------|
| `data_preprocessed/df_final.csv` | Integrated monthly panel: 119 districts × months (2005-2023), 13 columns (see schema). Contains the restricted dengue case counts. | Restricted - not included in this repository. Access must be requested from the Ministry of Health of the Republic of Indonesia (Kemenkes RI). |
| `df_centroid.csv` | District centroid coordinates (`Kab/Kota`, `longitude`, `latitude`). Derived from public HDX boundaries. | Included in this repository. |
| `indonesia_kabupaten.geojson` | District administrative boundaries for Java. | Public - included in this repository. |

## Schema of df_final.csv

| Column | Description |
|---|---|
| `Provinsi` | Province name. |
| `Kab/Kota` | District/municipality name. |
| `Year_Month` | Monthly observation period. |
| `Tahun` | Year. |
| `Kasus_DBD` | Monthly confirmed dengue case counts (restricted). |
| `Jumlah_Penduduk` | District population (BPS). |
| `DIR` | Dengue incidence rate per 100,000 population. |
| `DIR_log` | Log-transformed dengue incidence rate. |
| `longitude` | District centroid longitude. |
| `latitude` | District centroid latitude. |
| `temp_mean` | Monthly mean temperature from ERA5-Land. |
| `humidity_mean` | Monthly mean relative humidity from ERA5-Land. |
| `precip_sum` | Monthly accumulated precipitation from ERA5-Land. |

## Data sources and access

- **Dengue case surveillance (Kemenkes RI).** Restricted. The dengue surveillance data are not included in this repository and are not redistributed. Researchers seeking access should contact the Ministry of Health of the Republic of Indonesia (Kemenkes RI) and follow the applicable data access and authorization procedures. All case-count data derived from the restricted surveillance dataset have been removed from the notebooks and generated outputs.
- **Climate - ERA5 Land (Copernicus CDS).** Openly available from the Copernicus
  Climate Data Store: https://cds.climate.copernicus.eu/
- **Population - BPS (Statistics Indonesia).** Openly available: https://www.bps.go.id/
- **Administrative boundaries - HDX.** The district-level administrative boundary GeoJSON used in this study is included in this repository as indonesia_kabupaten.geojson.

## Reproducing the public portions

## Reproducing the public portions

The provided `indonesia_kabupaten.geojson` contains the public administrative
boundaries used in this study, and `df_centroid.csv` contains the corresponding
district centroid coordinates.

The restricted `df_final.csv` is required for the dengue modelling workflow.
Only the modelling steps that use `Kasus_DBD` and `DIR` require access to the
restricted surveillance data.
