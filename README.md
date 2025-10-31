# 🛰️ Crawl_Trace: Automated Detection and Tracing of Linear Landforms Using LiDAR

**Version:** 1.0 — *October 2025*  
**Author:** M. Jaweed Nazary, PhD Candidate  
**Affiliation:** Department of Civil and Environmental Engineering, University of Missouri — Columbia  
**Supported by:** EPA Grant No. CD97790701  
**Contact:** [mnxvx@umsystem.edu](mailto:mnxvx@umsystem.edu)

---

## 📘 Overview

**Crawl_Trace** is a Python-based tool that automatically detects, traces, and characterizes **levee-like** or **channel-like** linear landforms from **high-resolution LiDAR** data.  
It operates on a **1000 m × 1000 m** study tile centered at a user-defined location and employs a “crawling” algorithm that follows elevation gradients either **uphill** or **downhill**, depending on the selected tracing method.

This tool supports applications in:
- Wetland restoration and reconnection studies  
- Hydrological modeling and floodplain analysis  
- Geomorphometric and terrain pattern mapping  

---

## 🧠 Background

Traditional detection of small levees and channels from LiDAR involves **manual inspection** or **fixed thresholding** of DEM derivatives (e.g., slope, curvature).  
**Crawl_Trace** introduces an adaptive approach that:

- Randomly seeds multiple starting points across the study tile  
- Analyzes the **local elevation gradient** and **orientation**  
- “Crawls” along likely ridge or depression paths  
- Outputs **vectorized linear traces** representing probable geomorphic features  

This balance of automation and interpretability makes it suitable for **landscape-scale levee mapping** and **wetland hydrologic connectivity** analysis.

---

## 🚀 Example Usage

```python
from crawl_trace import Crawl_Trace

features = Crawl_Trace(
    location=(-10523769.57, 4719384.06),
    N=100,
    min_height=0.5,
    max_height=50.0,
    window_size=(100.0, 5.0),
    D=20.0,
    r=20.0,
    resolution=1,
    method=1,
    random_seed=59
)


Absolutely 👍 — here’s a **complete, GitHub-optimized README.md** version of your Crawl_Trace documentation.
This version includes all necessary sections: installation, usage, parameters, troubleshooting, and citation — all formatted 100% in Markdown so you can **copy and paste directly** into your GitHub repository’s `README.md`.

---

````markdown
# 🛰️ Crawl_Trace: Automated Detection and Tracing of Linear Landforms Using LiDAR

**Version:** 1.0 — *October 2025*  
**Author:** M. Jaweed Nazary, PhD Candidate  
**Affiliation:** College of Engineering, University of Missouri — Columbia  
**Supported by:** EPA Grant No. CD97790701  
**Contact:** [mnxvx@umsystem.edu](mailto:mnxvx@umsystem.edu)

---

## 📘 Overview

**Crawl_Trace** is a Python-based tool that automatically detects, traces, and characterizes **levee-like** or **channel-like** linear landforms from **high-resolution LiDAR** data.  
It operates on a **1000 m × 1000 m** study tile centered at a user-defined location and employs a “crawling” algorithm that follows elevation gradients either **uphill** or **downhill**, depending on the selected tracing method.

### Applications
- Wetland restoration and reconnection studies  
- Hydrological modeling and floodplain analysis  
- Geomorphometric and terrain feature mapping  

---

## 🧠 Background

Traditional methods for identifying levees and channels from LiDAR often rely on **manual interpretation** or **threshold-based filtering** of DEM derivatives (e.g., slope, curvature).  
**Crawl_Trace** introduces an adaptive, semi-randomized crawling algorithm that:

- Randomly seeds multiple starting points across the study tile  
- Analyzes the **local elevation gradient** and **orientation**  
- “Crawls” along ridge-like or depression-like paths  
- Produces **vectorized linear traces** representing potential geomorphic features  

This method balances **automation** and **interpretability**, making it suitable for **landscape-scale levee mapping** and **wetland hydrological connectivity** research.

---

## ⚙️ Installation

### Prerequisites

Ensure that you have Python **3.9+** installed.

### Required Libraries

```bash
pip install numpy geopandas matplotlib shapely rasterio pdal tqdm
````

> Note: PDAL must be properly installed and accessible in your environment.
> For system-level installation, visit: [https://pdal.io/download.html](https://pdal.io/download.html)

### Clone Repository

```bash
git clone https://github.com/<your-username>/Crawl_Trace.git
cd Crawl_Trace
```

---

## 🚀 Example Usage

```python
from crawl_trace import Crawl_Trace

features = Crawl_Trace(
    location=(-10523769.57, 4719384.06),
    N=100,
    min_height=0.5,
    max_height=50.0,
    window_size=(100.0, 5.0),
    D=20.0,
    r=20.0,
    resolution=1,
    method=1,
    random_seed=59
)

# The result is a GeoDataFrame of traced features
print(features.head())
```

**Crawl_Trace** retrieves LiDAR data for the specified location, initializes random seeds, performs iterative terrain crawling, and returns a **GeoPandas GeoDataFrame** containing traced linear features with their attributes.

---

## 🧩 Parameter Reference

| Parameter     | Type                | Description                                                                | Example                      |
| ------------- | ------------------- | -------------------------------------------------------------------------- | ---------------------------- |
| `location`    | tuple(float, float) | Center coordinates of the study tile (EPSG:3857)                           | `(-10523769.57, 4719384.06)` |
| `N`           | int                 | Number of random seed points. Higher values increase coverage and runtime. | `100`                        |
| `min_height`  | float               | Minimum relative elevation (m) for valid features.                         | `0.5`                        |
| `max_height`  | float               | Maximum relative elevation (m) for valid features.                         | `50.0`                       |
| `window_size` | tuple(float, float) | Local tracing window (length, width) in meters.                            | `(100.0, 5.0)`               |
| `D`           | float               | Offset distance (m) for advancing along feature direction.                 | `20.0`                       |
| `r`           | float               | Neighborhood radius (m) for local orientation estimation.                  | `20.0`                       |
| `resolution`  | int                 | LiDAR DEM processing resolution (m).                                       | `1`                          |
| `method`      | int                 | Tracing mode: `1 = uphill (levees)` or `2 = downhill (channels)`           | `1`                          |
| `random_seed` | int                 | Seed for reproducibility.                                                  | `59`                         |

---

## 📤 Output Description

**Returns:** `GeoDataFrame`

Each record corresponds to a traced linear feature point and includes:

* Relative elevation
* Tracing method (uphill/downhill)
* Feature height
* Directional anisotropy
* Normalized anisotropy
* Orientation angle (radians)

*Future versions will include attributes such as flow accumulation, leveed area, and feature confidence level.*

---

## 🧭 Recommended Workflow

1. **Coordinate System:** Ensure inputs are in **EPSG:3857** (units in meters).
2. **Divide Study Area:** Split your study region into **1000 × 1000 m tiles**.
3. **Parameter Tuning:** Calibrate parameters (`r`, `window_size`, `N`, `min_height`) on one test tile.
4. **Validation:** Overlay results on DEM or hillshade layers to visually confirm accuracy.
5. **Cross-Check:** Compare with existing datasets (e.g., **National Levee Dataset**).

> **Tip:** The algorithm often detects levees not listed in NLD — this is expected and beneficial for restoration studies.

---

## 🧰 Troubleshooting

| Error / Issue                         | Possible Cause                      | Suggested Fix                                |
| ------------------------------------- | ----------------------------------- | -------------------------------------------- |
| `ValueError: Invalid parameter types` | Incorrect coordinate format         | Ensure `location` uses `(x, y)` in EPSG:3857 |
| No features detected                  | Parameters too restrictive          | Decrease `min_height` or increase `N`        |
| Trace ends prematurely                | DEM too coarse or sparse            | Increase `r` or check LiDAR point density    |
| PDAL pipeline failure                 | Incorrect file path or missing data | Verify LiDAR availability and CRS            |

---

## 🧪 Example Workflow

```python
# Example batch processing of multiple tiles
import geopandas as gpd
import pandas as pd

tile_centers = [(-10523769.57, 4719384.06), (-10523800.21, 4719400.55)]

all_features = []

for loc in tile_centers:
    gdf = Crawl_Trace(
        location=loc,
        N=150,
        min_height=0.3,
        max_height=60.0,
        window_size=(120, 6),
        D=25,
        r=25,
        resolution=1,
        method=1,
        random_seed=42
    )
    all_features.append(gdf)

merged = gpd.GeoDataFrame(pd.concat(all_features, ignore_index=True))
merged.to_file("traced_features.shp")
```

---

## 📚 Citation

Citation details will be provided following publication of the related research paper.
Until then, please cite as:

> Nazary, M. J. (2025). *Crawl_Trace: Automated Detection and Tracing of Linear Landforms Using LiDAR*.
> College of Engineering, University of Missouri — Columbia.

---

## 🪪 License

MIT License
Copyright (c) 2025 M. Jaweed Nazary

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...

---

## 🌎 Acknowledgments

This work was supported by the **U.S. Environmental Protection Agency (EPA)** under Grant No. **CD97790701**.
Special thanks to the **University of Missouri — Columbia** for technical support and collaboration.

---

## 🧭 Keywords

`LiDAR` · `Levee Mapping` · `Channel Detection` · `Geomorphometry` · `Wetland Restoration` · `PDAL` · `Python`

````

