# Patterns of Urban Mobility: Explainable Clustering of Seoul's Bike-Share Stations

**CDS 303: Scientific Data Mining · Final Project · Team 8**
Dae Yeong Mun · Oscar Molina Romualdo

An explainable cluster analysis of Seoul's public bike-share system, **Ttareungi (따릉이)**, using 18.5 million trip records from January–June 2026.

**Project website:** <https://daeyeong-mun.github.io/CDS-303-Final-project/>

---

## Research question

What distinct usage profiles do Seoul's Ttareungi bike-share stations show from January to June 2026, and which behavioral characteristics best explain these differences?

The primary audience is the Seoul Metropolitan Government and Ttareungi operators. Understanding station usage patterns can support bicycle redistribution, station management, and future service planning.


## Approach

We follow the explainable cluster analysis framework of Alvarez-Garcia, Ibar-Alonso & Arenas-Parra (2024):

1. **Data preprocessing:** clean trips, handle missing values and outliers, build station-level features
2. **Dimensionality reduction:** drop highly correlated features, standardize, and apply PCA to find the main directions of station behaviour
3. **Clustering:** group stations with similar usage patterns
4. **Classification for explainability:** predict the cluster labels with a classifier and use SHAP values to describe what defines each cluster

## Repository layout

| Path | Contents |
|---|---|
| `docs/` | Written project sections, published as the project website with GitHub Pages |
| `notebooks/` | Jupyter notebooks with the supporting code |
| `figures/` | Figures used on the project pages |

## Project pages

| Section | Page |
|---|---|
| Project overview | [Overview](https://daeyeong-mun.github.io/CDS-303-Final-project/) |
| Paper summary | [Paper Summary](https://daeyeong-mun.github.io/CDS-303-Final-project/Paper%20Summary.html) |
| Variable selection | [Variables](https://github.com/DaeYeong-Mun/CDS-303-Final-project/blob/main/Variable%20Selection.md) |
| Supplementary dataset | [Supplementary Data](https://github.com/DaeYeong-Mun/CDS-303-Final-project/blob/main/Supplementary%20Dataset.md) |
| Principal Component Analysis | [PCA](https://daeyeong-mun.github.io/CDS-303-Final-project/PCA.html) |

## Data

| Dataset | Provider | Source |
|---|---|---|
| Public bike rental history (main dataset) | Seoul Metropolitan Government | [Seoul Open Data Plaza OA-15182](https://data.seoul.go.kr/dataList/OA-15182/F/1/datasetView.do) |
| Daily weather, ASOS station 108 (supplementary) | Korea Meteorological Administration | [KMA Open MET Data Portal](https://data.kma.go.kr/data/grnd/selectAsosRltmList.do?pgmNo=36) |

The full list of sources, including spatial context data, is on the [Supplementary Data page](https://daeyeong-mun.github.io/CDS-303-Final-project/supplementary-data.html#data-sources).

**Raw data files are not stored in this repository.** The main trip file is about 3.2 GB, well over GitHub's 100 MB file limit.
## Part 1: Data Integration and Preparation

### Data integration

The primary dataset contains 18,511,943 rental records from January to June 2026.

Rental records were aggregated by station ID and date and merged with 181 daily weather observations using the date as a common key. Station metadata was matched using station IDs.

Each row of the integrated daily dataset represents one station on one observed rental date. The final station-level dataset summarizes each station's rental behavior over the six-month study period.

### Data validation

| Validation metric | Result |
|---|---:|
| Total rental records | 18,511,943 |
| Weather observations | 181 |
| Missing weather dates | 0 |
| Duplicate weather dates | 0 |
| Station-date rows before integration | 492,721 |
| Station-date rows after integration | 492,721 |
| Duplicate station-date pairs | 0 |
| Unmatched weather records | 0 |
| Unique stations | 2,807 |
| Duplicate station IDs | 0 |
| Station IDs matched with location data | 2,807 |
| Missing English station names | 46 |

The integration preserved all 18,511,943 rental records in the aggregated rental counts without introducing duplicate station-date observations.

The station location dataset contains 77 invalid coordinates. These coordinates are excluded from spatial analysis.

### Rental count comparison

| Data source | Total rentals |
|---|---:|
| Individual rental records | 18,511,943 |
| Official daily rental summary | 17,978,991 |
| Difference | 532,952 |

The two sources differ by approximately 2.88% of the individual rental total. The exact reason remains unknown. The primary rental records are used consistently throughout the station-level analysis.

### Data preparation for PCA

Missing precipitation values were replaced with zero. Missing English station names were retained because station names are not PCA inputs.

Thirty stations with fewer than 50 rentals were excluded to reduce the influence of stations with limited activity.

Median trip distance was excluded due to its strong correlation with median trip duration (r = 0.91). Station identifiers, weather variables, and spatial variables were also excluded from PCA.

The ten selected behavioral variables were clipped at the 1st and 99th percentiles and standardized using StandardScaler to prevent differences in measurement scale from dominating the analysis.

| Final dataset | Result |
|---|---:|
| Stations before filtering | 2,807 |
| Stations excluded | 30 |
| Stations retained for PCA | 2,777 |
| Selected PCA variables | 10 |
| Missing PCA values | 0 |
| Infinite PCA values | 0 |

### Limitations

Weather observations represent citywide daily conditions rather than station-specific conditions. Seasonal effects and differences in station operating periods may influence rental activity.

Weather and spatial information are reserved for later analysis to help explain station usage profiles.

The full implementation and validation results are available in [Bike-S.ipynb](notebooks/Bike-S.ipynb).

## Running the notebooks

1. Download the datasets from the links above.
2. Place the CSV files in the same folder as the notebook. The raw Korean files are CP949-encoded, and the notebooks handle this.
3. Install the requirements: `pip install pandas numpy scikit-learn matplotlib seaborn scipy`. Later sessions will add more packages, such as `xgboost` and `shap`.
4. Run the notebook from top to bottom. The trip file is read in chunks, so it runs on a normal laptop; building the station features takes about one to two minutes.

Column names and category values are translated from Korean to English inside the notebooks.

