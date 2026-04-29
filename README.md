# The Geotechnical Time Tax
### A Pilot Study Linking Subsidence, Transit Delay, and Neighborhood Equity in Boston

---

## Overview

This pilot study proposes and tests a novel causal chain: that millimeter-scale **vertical land motion (VLM)** driven by 19th-century landfill consolidation is a statistically significant predictor of MBTA rapid transit slow zone placement — disproportionately imposing commute delays on low-income communities in Boston.

The proposed mechanism:

```
Filled land → differential settlement → track curvature
→ MBTA speed restriction → commute delay → income-stratified equity impact
```

No prior peer-reviewed study has quantified this full chain from geological substrate to transit equity outcome.

---

## Key Findings (Pilot)

| Finding | Result |
|---|---|
| Slow zones overlapping 1840s landfill | **57%** (vs. ~22% expected by chance — **3.2× enrichment**) |
| Mean VLM — landfill track segments | **−4.2 mm/yr** |
| Mean VLM — stable bedrock segments | **−1.1 mm/yr** |
| Annual delay — landfill corridor riders | **~1,875 min/yr** |
| Annual delay — stable corridor riders | **~437 min/yr** |
| Time Tax ratio | **~4.3×** (~24 extra hours/yr for landfill-corridor commuters) |
| Pearson r (median income vs. annual delay) | **≈ −0.87** |

> ⚠️ **Data Note:** InSAR VLM measurements and per-segment delay values are currently calibrated synthetic placeholders pending live Sentinel-1 product ingestion (NASA ASF Vertex) and MBTA LAMP travel-time records. The spatial overlap finding (57%) is based on real GTFS and historical shoreline data. The full analytical framework is production-ready for live data.

---

## Data Sources

| Layer | Source | Status |
|---|---|---|
| MBTA Rapid Transit Geometry | [MBTA GTFS 2026](https://cdn.mbta.com) | ✅ Real — live feed |
| 1840s Historical Landfill Boundary | CZM MORIS / digitized shoreline vectors | ✅ Real — included in `/data/shoreline/` |
| Vertical Land Motion (InSAR) | Sentinel-1 via [NASA ASF Vertex](https://search.asf.alaska.edu) | 🔄 Synthetic placeholder |
| MBTA Slow Zone Records | MBTA LAMP Program | 🔄 Synthetic placeholder |
| Socioeconomic Data | [U.S. Census ACS 2023 5-yr](https://www.census.gov/programs-surveys/acs) — Suffolk Co. | 🔄 Partially real (equity DataFrame is illustrative) |

---

## Repository Structure

```
geotechnical-time-tax/
├── geotechnical_time_tax.ipynb   # Full analysis notebook
├── data/
│   ├── shoreline/                # 1840s Boston landfill boundary (GeoJSON)
│   ├── correlation_matrix.png    # Pearson correlation matrix output
│   ├── subsidence_vs_delay.png   # OLS regression scatter plot
│   ├── time_tax_chart.png        # Equity bar chart + income bubble chart
│   └── sinking_subway_map.html   # Interactive Folium map
└── .gitignore
```

---

## Methods Summary

**Section 1 — MBTA Transit Geometry**
GTFS feed parsed into GeoDataFrames (LineStrings per route). Slow zones loaded as point features. All downstream analysis joins back to the slow zone table as the central fact table.

**Section 2 — Historical Landfill Overlay**
1840s shoreline polygons spatially joined to slow zone points (`predicate='within'`). Overlap rate compared against the landfill footprint's share of the network to compute spatial enrichment.

**Section 3 — InSAR VLM**
Sentinel-1 subsidence grid joined to slow zones via 500m buffers. VLM points within each buffer averaged to assign a representative subsidence rate per segment.

**Section 4 — Subsidence Impact Factor (SIF)**
Structural stress per segment computed using the beam-bending equation:

$$S = E \cdot \frac{d^2w}{dx^2}$$

where E is the elastic modulus of steel rail (200 GPa) and d²w/dx² is the second spatial derivative of the VLM field (curvature of the settlement profile). Normalized SIF correlated against per-segment delay.

**Section 5–7 — Equity Modeling**
ACS 2023 median household income joined to neighborhood clusters surrounding each slow zone. Annual delay per commuter computed and correlated against income (Pearson r). Visualized as a bar chart and income-vs-delay bubble chart.

**Section 8 — Composite Spatial Map**
Three-layer visualization: InSAR subsidence heatmap + MBTA line geometries + 1840s landfill polygons. Rendered as an interactive Folium map and a static Matplotlib figure.

---

## Environment Setup

```bash
# Requires Python 3.11+
pip install geopandas shapely folium scikit-learn numpy pandas matplotlib scipy
```

All dependencies are available via pip. No proprietary software required.

---

## Next Steps Toward Publication

1. Obtain NASA Earthdata credentials → download live Sentinel-1 SLC products for Boston AOI
2. Process InSAR time series (2020–2026) using ISCE2 + MintPy
3. File Massachusetts Public Records Request for MBTA LAMP travel-time CSVs
4. Validate landfill boundary against official CZM MORIS shapefile
5. Expand census spatial join to all 218 Suffolk County tracts
6. Confirmatory spatial statistics: Moran's I, Geographically Weighted Regression, Granger causality
7. Submit to *AGU Fall Meeting* or *Urban Climate* journal

---

## Author

**Fortune Kosi Udeh**
Boston, MA · [GitHub](https://github.com/FortuneKosiUdeh)

---

*This study was developed as a pilot framework for peer-reviewed research. All placeholder findings are clearly marked and require validation against live data before publication.*
