<!-- ### TEXT BY CLAUDE ### -->
# Data sources

All data comes from the Israeli government data portal ([data.gov.il](https://data.gov.il)).
Raw files in this folder are never modified. Every cleaning or join step happens in code.

## Folder layout

```
data/
├── SOURCES.md                       this file
├── accid_taz.csv                    BASE dataset: one row per traffic zone (TAZ)
├── accid_taz.zip                    zone polygons (shapefile), used for the spatial join
├── accid_taz_kmz.zip                same polygons, KMZ format (for viewing only)
├── accid_taz_metadata.csv           column descriptions of the base dataset
└── external/                        enrichment datasets (joined onto the base)
    ├── traffic_light_junction.csv
    ├── traffic_light_junction_metadata.csv
    ├── roundabout.csv
    └── roundabout_metadata.csv
```

## 1. Base dataset: accidents by traffic zone

| | |
|---|---|
| Portal page | https://data.gov.il/he/datasets/ministry_of_transport/accid_taz |
| Publisher | Ministry of Transport and Road Safety |
| Last updated on portal | 2026-10-22 |
| Size | 2,637 zones × 29 columns, single snapshot (YEARMONTH = 202608) |
| Coordinate system (polygons) | Israel TM Grid (ITM) |

This dataset stays the basis of the project. The enrichment datasets only add features to it.

## 2. Enrichment: signalized junctions

| | |
|---|---|
| Portal page | https://data.gov.il/he/datasets/ministry_of_transport/traffic_light_junction |
| Publisher | Ministry of Transport and Road Safety |
| Last updated on portal | 2026-10-22 |
| Size | 3,241 junctions (one row per junction) |
| Location fields | `X`, `Y` in Israel TM Grid (same system as the zone polygons), plus `CITY`, `CITYCODE` |
| Retrieved | 2026-11-09, through the portal's datastore API |

## 3. Enrichment: roundabouts

| | |
|---|---|
| Portal page | https://data.gov.il/he/datasets/ministry_of_transport/roundabout |
| Publisher | Ministry of Transport and Road Safety |
| Last updated on portal | 2026-10-25 |
| Size | 8,642 roundabouts (one row per roundabout) |
| Location fields | `X`, `Y` in Israel TM Grid, plus `CITY`, `CITYCODE` |
| Retrieved | 2026-11-09, through the portal's datastore API |

## Join method (planned)

- **Spatial join:** each junction or roundabout point is assigned to the zone polygon that contains it (point in polygon).
- **Features per zone:** the number of signalized junctions and roundabouts, and their density per km².
- **Coordinates:** both layers use the same coordinate system, so no reprojection is needed.

## Leakage check

The enrichment features describe road infrastructure and contain no accident or injury counts, so they do not define the target. The relation may still run in the opposite direction: a traffic light may have been installed because of past accidents. Results will therefore be reported as associations, not causes.
<!-- #### -->
