# 🌍 Human Flourishing: Large-Scale Geo-Twitter Spatial Extraction Pipeline

A scalable, multi-threaded, high-performance geospatial data ingestion and filtering pipeline built to extract, validate, and organize global geolocated tweets from the **Harvard CGA (Center for Geographic Analysis)** global repository (~100,000 compressed day/hour archives; 2010–2023).

This module processes massive geospatial archives to support research in spatial artificial intelligence, urban mobility, and longitudinal studies of human flourishing across international regional study areas: **Israel (ISR)**, **China (CHN)**, and **Hong Kong (HKG)**.

---

## 📌 Features

- **Massive Archive Traversal**: Efficiently scans, indexes, and streams over **98,500+** gzip-compressed tab-separated archives spanning 2010 to 2023.
- **Two-Tier Spatial Filtering**:
  1. *Vectorized Bounding-Box Pruning*: Rapidly excludes out-of-bounds coordinates via high-speed NumPy/Pandas array operations.
  2. *Point-in-Polygon (PiP) Intersection*: Evaluates candidate coordinates with high topological accuracy using GeoPandas spatial indexing (`gpd.sjoin`) against official GADM administrative boundary shapefiles (`adm1` and `adm2`).
- **Parallel Multi-Core Architecture**: Utilizes Python's `multiprocessing.Pool` across high-performance compute clusters (up to 32 parallel worker nodes) with isolated worker memory heaps and garbage collection sweeps.
- **Robust Schema Normalization**: Parses and validates 24 tabular metadata columns (including coordinates, user metrics, device indicators, and timestamps) and maps them to administrative boundary identifiers (`ISO`, `ID_0`, `NAME_0`, `ID_1`, `NAME_1`, `ID_2`, `NAME_2`).
- **Storage-Optimized Export**:
  - Partitioned daily columnar records (`YYYY-MM-DD.parquet`) powered by **PyArrow**.
  - High-throughput fallback tables saved as compressed `.csv.gz`.

---

## 🗺️ Spatial Coverage & Geographies

| Region | ISO Alpha-3 | Target Admin Level | Spatial Filter Strategy |
| :--- | :---: | :---: | :--- |
| **Israel** | `ISR` | Level 1 (`adm1`) | Bounding Box + Polygons (Districts/Subdistricts) |
| **China** | `CHN` | Level 2 (`adm2`) | Bounding Box + Polygons (Prefectures/Cities) |
| **Hong Kong** | `HKG` | Level 1 (`adm1`) | Precise District Polygon Boundaries |

---
