# NOAA Storms Pipeline

A one-command pipeline that downloads a year of NOAA Storm Events data, converts it to GeoParquet, and lands it ready for analysis in DuckDB, GeoPandas, or QGIS.

## What it does

`pipeline.sh` takes a year (default: 2024), pulls the raw `details` file from NOAA's public archive, decompresses it, and converts it to a single GeoParquet file at `data/processed/storms_{YEAR}.parquet`.

Total runtime: about 90 seconds for a typical year on a home internet connection.

## The data

- **Source:** [NOAA Storm Events Database](https://www.ncei.noaa.gov/pub/data/swdi/stormevents/csvfiles/)
- **License:** Public domain (US federal data)
- **What's in it:** every recorded storm event in the United States for the given year, including type, location, and damages. d = date of the storm event, and c = when it was posted by NOAA.

## How to run it

Requires GDAL (for `ogr2ogr`) and standard Unix utilities (`curl`, `gunzip`).

```bash
git clone https://github.com/rosie-rgb
/noaa-storms-pipeline.git
cd noaa-storms-pipeline
chmod +x pipeline.sh
./pipeline.sh
```

To run for a specific year:

```bash
./pipeline.sh 2023
```

## What I learned

The hardest part was understanding how the tools fit together. Coming from a GUI-based ESRI workflow, I kept confusing the text editor (VS Code) with the terminal (Git Bash) — it clicked when I realized VS Code is just where you write, and Git Bash is where you run. I also ran into a working directory issue where Git Bash was executing the original starter file instead of my edited version, which taught me to always verify your path before running a script. Realizing how central GDAL is to the entire open source geospatial stack (powering QGIS, GeoPandas, and this pipeline all at once) made everything feel more connected and worth learning.

## Stack

- bash
- curl
- GDAL / ogr2ogr
- GeoParquet
