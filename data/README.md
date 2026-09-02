# Data directory

The notebooks in this repository expect the following files in `data/`. They are
**not committed** to the repository because the dengue case counts are restricted
(see below). They are listed here so the expected schema is clear and the code can
be re-run once access is obtained.

## Expected files

| File | Description | Availability |
|------|-------------|--------------|
| `data_preprocessed/df_final.csv` | Integrated monthly panel: 119 districts × months (2005–2024), 13 columns (see schema). Contains the restricted dengue case counts. | **Restricted** - request from the Indonesian Ministry of Health (Kemenkes RI). |
| `df_centroid.csv` | District centroid coordinates (`Kab/Kota`, `longitude`, `latitude`). Derived from public HDX boundaries. | Reproducible from the public GeoJSON (see below). |
| `indonesia_kabupaten.geojson` | District administrative boundaries for Java. | **Public** - downloaded automatically by the notebook from HDX. |

## Schema of `df_final.csv`

```
Provinsi, Kab/Kota, Year_Month, Tahun, Kasus_DBD, Jumlah_Penduduk,
DIR, DIR_log, longitude, latitude, temp_mean, humidity_mean, precip_sum
```

- `Kasus_DBD` - monthly confirmed dengue case counts (**restricted**).
- `Jumlah_Penduduk` - district population (BPS).
- `DIR`, `DIR_log` - dengue incidence rate per 100,000 and its log transform.
- `temp_mean`, `humidity_mean`, `precip_sum` - monthly climate aggregates (ERA5-Land).

## Data sources and access

- **Dengue case surveillance (Kemenkes RI).** Restricted. The raw and integrated
  case data cannot be redistributed. Researchers may request access directly from
  the Ministry of Health of the Republic of Indonesia. All derived case counts have
  been removed from the notebooks and outputs in this repository.
- **Climate - ERA5-Land (Copernicus CDS).** Openly available from the Copernicus
  Climate Data Store: https://cds.climate.copernicus.eu/
- **Population — BPS (Statistics Indonesia).** Openly available: https://www.bps.go.id/
- **Administrative boundaries - HDX.** Openly available; the notebook downloads the
  Java district GeoJSON automatically on first run.

## Reproducing the public portions

`df_centroid.csv` and `indonesia_kabupaten.geojson` can be regenerated from the
public HDX GeoJSON without any restricted data. Only the modelling steps that use
`Kasus_DBD` / `DIR` require the restricted file.
