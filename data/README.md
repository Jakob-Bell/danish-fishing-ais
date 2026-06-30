# Data

The datasets used in this project are **not committed to the repository** — they are far too
large for GitHub (hundreds of MB to multiple GB). The folders below are git-ignored. Download
or regenerate the data locally and the notebooks will pick it up automatically.

```
data/
├── raw/        # Raw AIS point data, one Parquet file per year  (download — step 1)
├── fishing/    # Fishing-vessel-only Parquet, produced by notebook 01  (step 2)
└── N2000/      # Natura 2000 protected-area shapefiles  (download — step 3)
```

## 1. Raw AIS data → `data/raw/`

Source: **Danish Maritime Authority (Søfartsstyrelsen)** AIS archive
👉 https://www.dma.dk/safety-at-sea/navigational-information/ais-data

Download the yearly archives and place the Parquet files here using the naming pattern the
notebooks expect:

```
data/raw/aisdk-2021-1h.parquet
data/raw/aisdk-2022-1h.parquet
...
data/raw/aisdk-2026-1h.parquet
```

> The official archive ships as daily CSVs. We pre-aggregated them to hourly Parquet
> (`-1h`) for speed. A single national file holds 100M+ rows, so always use Polars'
> `scan_parquet` lazy API — see [`../docs/BIG_DATA_TIPS.md`](../docs/BIG_DATA_TIPS.md).

## 2. Fishing-only data → `data/fishing/`

Don't download these — **generate them** by running
[`../notebooks/01_data_preparation.ipynb`](../notebooks/01_data_preparation.ipynb), which
filters each raw file down to fishing vessels and writes:

```
data/fishing/fishing_aisdk-<year>-1h.parquet
```

## 3. Natura 2000 protected areas → `data/N2000/`

Source: **Danish Environmental Protection Agency** Natura 2000 / MiljøGIS shapefiles.
The analysis in notebook 03 uses `np3_2022_marine_kortlaeg_2004_2018.shp` (and its sidecar
`.shx` / `.dbf` / `.prj` files). Place the full shapefile set in `data/N2000/`.
