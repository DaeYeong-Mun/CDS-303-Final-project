# CDS 303 Final Project

## Team 8

**Team Members:**
- Dae Yeong Mun
- Oscar Molina Romualdo

## Project Title
Explainable Cluster Analysis of Seoul Public Bicycle Rental Patterns

## Project Overview
This project aims to identify and explain different usage patterns in Seoul's public bicycle rental system, Ttareungi. We will use data preprocessing, dimensionality reduction, clustering, and classification to analyze how rental stations differ based on when they are used, how long their trips are, and who rides from them. By identifying groups of stations with similar usage, we hope to better understand how public bicycles are used in Seoul.

## Research Question
Can Seoul's public bicycle rental stations be grouped into distinct usage patterns based on time-of-day patterns, weekday/weekend balance, trip length, and rider mix, and what characteristics, including sensitivity to weather, explain these groups?

## Dataset Description
Our primary dataset is the Seoul Public Bicycle (Ttareungi) Rental History, obtained from the Seoul Open Data Plaza. It contains 18,511,943 rental records collected from January 1 to June 30, 2026, with 16 variables. These include rental and return times, rental stations, trip duration, travel distance, birth year, gender, and user type.

Each record in the dataset is a single trip. Because our unit of analysis is the station, we will aggregate the trip records for each rental station into station-level features before clustering.

- **Provider:** Seoul Metropolitan Government, via Seoul Open Data Plaza
- **Source:** <https://data.seoul.go.kr/dataList/OA-15182/F/1/datasetView.do>
- **Licence:** Korea Open Government License (KOGL) Type 1, attribution required

The original column names are in Korean and are translated to English in our notebook, [Bike-S.ipynb](https://github.com/Oscarmvr-12/Seoul-Bike/blob/main/notebooks/Bike-S.ipynb), which loads the full trip dataset and reports its first rows, shape, columns, data types, summary statistics, and missing values.

## Project Sessions
- Session 1: Research Planning and Dataset Exploration
- Future Sessions: To be updated

## Session 1: Research Planning and Dataset Exploration

### Project Documents

1. [Paper Summary](https://daeyeong-mun.github.io/CDS-303-Final-project/Paper%20Summary.html)
2. [Variable Selection Table](https://daeyeong-mun.github.io/CDS-303-Final-project/Variable%20Selection.html)
3. [Supplementary Dataset](https://daeyeong-mun.github.io/CDS-303-Final-project/Supplementary%20Dataset.html)

### Future Sessions

Additional project updates and analysis results will be added here as the project progresses.
