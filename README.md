# Patterns of Urban Mobility: Explainable Clustering of Seoul's Bike-Share Stations

**CDS 303: Scientific Data Mining · Final Project · Team 8**
Dae Yeong Mun · Oscar Molina Romualdo

An explainable cluster analysis of Seoul's public bike-share system, **Ttareungi (따릉이)**, using 18.5 million trip records from January–June 2026.

**Project website:** <https://daeyeong-mun.github.io/CDS-303-Final-project/>

---

## Research question

> What distinct usage profiles do Seoul's Ttareungi bike-share stations show in January–June 2026, and which characteristics best explain those profiles: time-of-day patterns, weekday/weekend balance, trip length, rider mix and sensitivity to weather?

**Unit of analysis:** the rental station. Trip-level records are aggregated into station-level features.

## Approach

We follow the explainable cluster analysis framework of Alvarez-Garcia, Ibar-Alonso & Arenas-Parra (2024):

1. **Data preprocessing:** clean trips, handle missing values and outliers, build station-level features
2. **Dimensionality reduction:** remove redundant features, or reduce them if needed
3. **Clustering:** group stations with similar usage patterns
4. **Classification for explainability:** predict the cluster labels with a classifier and use SHAP values to describe what defines each cluster

## Repository layout

| Path | Contents |
|---|---|
| `docs/` | Written project sections, published as the project website with GitHub Pages |
| `notebooks/` | Jupyter notebooks with the supporting code |

## Project pages (Session 1)

| Section | Page |
|---|---|
| Project overview | [Overview](https://daeyeong-mun.github.io/CDS-303-Final-project/) |
| Paper summary | [Paper Summary](https://github.com/DaeYeong-Mun/CDS-303-Final-project/blob/main/Paper%20Summary.md) |
| Variable selection | [Variables](https://github.com/DaeYeong-Mun/CDS-303-Final-project/blob/main/Variable%20Selection.md) |
| Supplementary dataset | [Supplementary Data](https://github.com/DaeYeong-Mun/CDS-303-Final-project/blob/main/Supplementary%20Dataset.md) |

## Data

| Dataset | Provider | Source |
|---|---|---|
| Public bike rental history (main dataset) | Seoul Metropolitan Government | [Seoul Open Data Plaza OA-15182](https://data.seoul.go.kr/dataList/OA-15182/F/1/datasetView.do) |
| Daily weather, ASOS station 108 (supplementary) | Korea Meteorological Administration | [KMA Open MET Data Portal](https://data.kma.go.kr/data/grnd/selectAsosRltmList.do?pgmNo=36) |

The full list of sources, including spatial context data, is on the [Supplementary Data page](https://daeyeong-mun.github.io/CDS-303-Final-project/supplementary-data.html#data-sources).

**Raw data files are not stored in this repository.** The main trip file is about 3.1 GB, well over GitHub's 100 MB file limit.

## Running the notebooks

1. Download the datasets from the links above.
2. Place the CSV files in the same folder as the notebook. The raw Korean files are CP949-encoded, and the notebooks handle this.
3. Install the requirements: `pip install pandas numpy scikit-learn`. Later sessions will add more packages, such as `xgboost` and `shap`.
4. Run the notebook from top to bottom. Loading the full trip file can take a few minutes and needs several GB of RAM.

Column names and category values are translated from Korean to English inside the notebooks.

