# Shanghai Real Estate Prices & Subway Proximity

Does living close to the subway make an apartment more expensive in Shanghai, and by how much per metre?

Geospatial analysis of **~450,000 real estate listings** (Anjuke, 2017) cross-referenced with **subway station entrances** (Gaode POI, 2017).

*Course project, TSH00, UTSEUS (Shanghai University).*

## Approach

1. **Cleaning** the listings: type conversion, removal of incomplete rows, filtering of listings outside Shanghai with a bounding box
2. **Geospatial processing** with GeoPandas: point geometries, coordinate-system check on a basemap
3. **Subway entrances** extracted from the Gaode POI database (national GB code 200402)
4. **Distance** from each apartment to the nearest subway entrance (vectorised with Shapely)
5. **OLS regression** of the price per m² on the distance (statsmodels), with residual analysis

## Results

| | Value |
|---|---|
| Observations | 449,514 |
| R² | 0.175 |
| Effect of distance | ≈ **−2 ¥/m² per metre** (≈ −2,000 ¥/m² per km) |
| p-value | < 0.001 |

An apartment next to a subway entrance is estimated at about 67,600 ¥/m², compared with about 57,000 ¥/m² at 5 km.

**Limits:** distance to the subway alone explains only 17.5% of price variance, and residuals show strong spatial autocorrelation (Durbin–Watson = 0.56). Distances were computed in degrees and converted approximately (1° ≈ 100 km). Next steps: metric projection, distance to the city centre, district fixed effects, log price.

## Data

The datasets (Anjuke listings collected by UTSEUS, Gaode POI licensed to Shanghai University) were provided for the course and **are not redistributed** here. The notebook expects them in `data/`.

```bash
pip install -r requirements.txt
jupyter notebook shanghai_real_estate_subway.ipynb
```
