# CDS 303 Final Project

## Team 8

**Team Members:**
- Dae Yeong Mun
- Oscar Molina Romualdo

## Project Title
Patterns of Urban Mobility: Explainable Clustering of Seoul’s Bike-Share Stations

## Project Overview
This project aims to identify and explain different usage patterns in Seoul's public bicycle rental system, Ttareungi. We will use data preprocessing, dimensionality reduction, clustering, and classification to analyze how rental stations differ based on when they are used, how long their trips are, and who rides from them. By identifying groups of stations with similar usage, we hope to better understand how public bicycles are used in Seoul.

## Research Question
How do bicycle rental patterns vary across time periods, weather conditions, and rental stations in Seoul, and what underlying dimensions of usage variation can Principal Component Analysis (PCA) reveal?

## Dataset Description
Our primary dataset is the Seoul Public Bicycle (Ttareungi) Rental History, obtained from the Seoul Open Data Plaza. It contains 18,511,943 rental records collected from January 1 to June 30, 2026, with 16 variables. These include rental and return times, rental stations, trip duration, travel distance, birth year, gender, and user type.

Each record in the dataset is a single trip. Because our unit of analysis is the station, we will aggregate the trip records for each rental station into station-level features before clustering.

- **Provider:** Seoul Metropolitan Government, via Seoul Open Data Plaza
- **Source:** <https://data.seoul.go.kr/dataList/OA-15182/F/1/datasetView.do>
- **Licence:** Korea Open Government License (KOGL) Type 1, attribution required

The original column names are in Korean and are translated to English in our notebook, [Bike-S.ipynb](https://github.com/DaeYeong-Mun/CDS-303-Final-project/blob/main/notebooks/Bike-S.ipynb), which loads the full trip dataset and reports its first rows, shape, columns, data types, summary statistics, and missing values.

## Project Sessions
- Research Planning and Dataset Exploration
- Station Features and Principal Component Analysis

## Research Planning and Dataset Exploration

### Project Documents

1. [Paper Summary](https://daeyeong-mun.github.io/CDS-303-Final-project/Paper%20Summary.html)
2. [Variable Selection Table](https://daeyeong-mun.github.io/CDS-303-Final-project/Variable%20Selection.html)
3. [Supplementary Dataset](https://daeyeong-mun.github.io/CDS-303-Final-project/Supplementary%20Dataset.html)

#### Project Sessions

- Research Planning and Dataset Exploration
- Data Integration and Preparation
- Station Features and Principal Component Analysis

#### Data Integration and Preparation

We integrated 18,511,943 bicycle rental records with 181 daily weather observations from January to June 2026.

The integration produced 492,721 unique station-date observations without duplicate rows, unmatched weather records, or changes in total rental counts.

After excluding 30 stations with fewer than 50 rentals, the final PCA dataset contains 2,777 stations and 10 standardized behavioral variables, with no missing or infinite values.

[Full Data Integration and Validation Results](https://github.com/DaeYeong-Mun/CDS-303-Final-project/blob/main/README.md#part-1-data-integration-and-preparation)

##  Station Features and Principal Component Analysis

We aggregated the 18.5 million trips into station-level features and applied PCA to 10 of them for 2,777 stations. Four components explain 81% of the variance: home end vs. work end of the commute, leisure vs. everyday use, night-time use, and station size. Weather sensitivity was moved to an analysis after clustering, because linking daily weather to six-month station summaries mixes weather with season and holidays.

1. [Principal Component Analysis](https://daeyeong-mun.github.io/CDS-303-Final-project/PCA.html)
2. [Variable Selection Table (updated)](https://daeyeong-mun.github.io/CDS-303-Final-project/Variable%20Selection.html)

