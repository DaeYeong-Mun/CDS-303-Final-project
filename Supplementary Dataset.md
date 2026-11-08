# Supplementary Dataset

## 1. Dataset Information

Dataset Title: Synoptic Weather Observation Data (ASOS), daily

Provider: Korea Meteorological Administration (KMA), Open MET Data Portal

Source: https://data.kma.go.kr/data/grnd/selectAsosRltmList.do?pgmNo=36 (free account login required to download)

Planned Study Period: January 1, 2026 to June 30, 2026 (181 days)

Location: Seoul, South Korea (station 108)

File in our project: seoul_weather_2026_01-06.csv (181 rows, one per day)

Accessed: November 3, 2026

## 2. Dataset Description

For our supplementary dataset, we selected daily weather observation data provided by the Korea Meteorological Administration. This dataset contains weather measurements collected at observation stations in South Korea.

We use observations from the Seoul station during the same period as our primary bicycle rental dataset. The weather data can provide additional information about the environmental conditions on each day of bicycle rentals.

## 3. Relevant Variables

| Variable | Description | Unit | Proposed Use |
|---|---|---|---|
| date (일시) | Date of weather observation | Date | Connect weather data with rental records |
| avg_temp_c (평균기온) | Daily mean air temperature (−9.7 to 27.2 in our data) | Celsius | Examine rental patterns under different temperatures |
| min_temp_c, max_temp_c (최저/최고기온) | Daily minimum and maximum temperature | Celsius | Identify freezing days for cold sensitivity |
| precip_mm (일강수량) | Daily precipitation; blank on 120 days with no measurable precipitation, which we fill with 0 | mm | Investigate differences between rainy and dry days |
| avg_wind_mps (평균 풍속) | Daily mean wind speed | m/s | Examine the relationship between wind and bicycle usage |
| avg_humidity_pct (평균 상대습도) | Daily mean relative humidity | Percent | Provide additional environmental context |
| sunshine_hr (합계 일조시간) | Total daily sunshine | Hours | Provide additional environmental context |
| station_id, station_name_kr (지점, 지점명) | Observation station (constant: 108, 서울) | — | Excluded from analysis |

## 4. Contribution to Our Research Question

Our main research question focuses on identifying different station usage patterns based on time of use, trip length, and rider mix.

Weather conditions may help explain why these patterns differ. For example, stations used mainly for weekday commuting may hold up better on rainy or cold days, while leisure-oriented stations may see much lower use in bad weather.

By comparing weather sensitivity across the identified clusters, we hope to understand whether environmental factors are related to different bicycle usage patterns.

This additional information could make our clustering results easier to interpret.

## 5. Connection to Our Primary Dataset

Our primary dataset contains bicycle rental timestamps, while the supplementary dataset provides one weather observation per day.

We plan to connect the two datasets using the date. First, we will extract the rental date from rental_datetime. Next, each trip will be matched to that day's weather row. The weather file has exactly one row for each of the 181 days in the rental data, with no missing dates.

Before merging, we will check date formats, missing values, and duplicate weather records.

Since the weather observations come from a single station, we will also consider the limitations of using one Seoul observation station to represent conditions across the entire city.

## 6. Planned Use in Our Analysis

Because the weather data is city-wide and daily, it cannot be merged directly as a station-level column: every station would get identical values on a given day. Instead, we plan to:

1. Join trips to daily weather by date.
2. Aggregate for each station into weather-sensitivity features, such as a station's average daily rentals on rainy days divided by its average on dry days.
3. Use those features mainly to interpret the clusters: described for each cluster after clustering, rather than used to form the clusters.

Known limitations:

- One observation point for the whole city, so local differences in weather are not captured.
- Only 15 days had a mean temperature below −5 °C, all in January–February. Any cold-sensitivity measure must therefore compare freezing and non-freezing days within January–February, so that seasonal growth in ridership is not mistaken for weather sensitivity.
- Rain gives more contrast: 61 days have a recorded precipitation value.

Actual data integration and analysis have not yet been completed. For Session 1, our goal is to identify a suitable supplementary dataset and explain how it could support our research.

## 7. Planned Context Datasets (Later Sessions)

These have been collected but are not part of the Session 1 analysis. They may be used later to interpret clusters.

| Dataset | Provider / Source | How It Would Connect | Possible Use |
|---|---|---|---|
| Ttareungi station information | Seoul Open Data Plaza, [OA-13252](https://data.seoul.go.kr/dataList/OA-13252/F/1/datasetView.do) | Station ID (rental_station_id ↔ 대여소_ID) | Coordinates for all spatial features; 77 stations with (0, 0) coordinates must be excluded |
| Seoul subway station master | Seoul Open Data Plaza, [OA-21232](https://data.seoul.go.kr/dataList/OA-21232/S/1/datasetView.do) | Distance from each bike station to the nearest subway station | First/last-mile interpretation |
| Seoul district boundaries | [datainworld/administrative_district](https://github.com/datainworld/administrative_district) (GitHub) | Point-in-polygon: which of the 25 districts a station is in | District labels for interpretation |
| District-level daily living population | Seoul Open Data Plaza, [OA-23031](https://data.seoul.go.kr/dataList/OA-23031/S/1/datasetView.do) | District + date | Coarse context only; the citywide total row (code 11000) must be removed |
| Seoul cycleway network | OpenStreetMap contributors, via Overpass Turbo ([ODbL](https://www.openstreetmap.org/copyright)) | Distance to the nearest cycleway | Infrastructure context; OSM coverage may be uneven |

## 8. Data Sources

| Dataset | Provider | Link | Licence |
|---|---|---|---|
| Public bike rental history (main dataset) | Seoul Metropolitan Government | [OA-15182](https://data.seoul.go.kr/dataList/OA-15182/F/1/datasetView.do) | KOGL Type 1 (attribution) |
| Public bike daily rental counts | Seoul Metropolitan Government | [OA-14994](https://data.seoul.go.kr/dataList/OA-14994/F/1/datasetView.do) | KOGL Type 1 (attribution) |
| Daily weather, ASOS station 108 | Korea Meteorological Administration | [data.kma.go.kr](https://data.kma.go.kr/data/grnd/selectAsosRltmList.do?pgmNo=36) | See KMA portal terms |
| Station information | Seoul Metropolitan Government | [OA-13252](https://data.seoul.go.kr/dataList/OA-13252/F/1/datasetView.do) | KOGL Type 1 (attribution) |
| Subway station master | Seoul Metropolitan Government | [OA-21232](https://data.seoul.go.kr/dataList/OA-21232/S/1/datasetView.do) | KOGL Type 1 (attribution) |
| District-level living population | Seoul Metropolitan Government | [OA-23031](https://data.seoul.go.kr/dataList/OA-23031/S/1/datasetView.do) | KOGL Type 1 (attribution) |
| District boundaries | datainworld (GitHub) | [repository](https://github.com/datainworld/administrative_district) | See repository |
| Cycleway network | © OpenStreetMap contributors | [openstreetmap.org](https://www.openstreetmap.org/copyright) | ODbL |

All sources accessed November 3, 2026. Raw data files are not stored in this repository because the main trip file (~3.1 GB) exceeds GitHub's file-size limit.

## 9. Conclusion

We selected daily weather observation data because it can provide useful environmental context for Seoul's public bicycle rental patterns.

Combining bicycle rental information with weather observations may help us better understand the characteristics of different station groups and make our clustering results more meaningful.
