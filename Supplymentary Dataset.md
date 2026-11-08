# Supplementary Dataset

## 1. Dataset Information

Dataset Title: Hourly Weather Observation Data (ASOS)

Provider: Korea Meteorological Administration (KMA)

Source: https://data.kma.go.kr/data/grnd/selectAsosRltmList.do?pgmNo=36

Planned Study Period: January 1, 2026 to June 30, 2026

Location: Seoul, South Korea

## 2. Dataset Description

For our supplementary dataset, we selected hourly weather observation data provided by the Korea Meteorological Administration. This dataset contains weather measurements collected at observation stations in South Korea.

We plan to use observations from Seoul during the same period as our primary bicycle rental dataset. The weather data can provide additional information about the environmental conditions during bicycle rentals.

## 3. Relevant Variables

| Variable | Description | Unit | Proposed Use |
|---|---|---|---|
| Observation Date and Time | Time of weather observation | Date and hour | Connect weather data with rental records |
| Temperature | Air temperature | Celsius | Examine rental patterns under different temperatures |
| Precipitation | Hourly precipitation | mm | Investigate differences between rainy and dry periods |
| Wind Speed | Observed wind speed | m/s | Examine the relationship between wind and bicycle usage |
| Relative Humidity | Amount of moisture in the air | Percent | Provide additional environmental context |

## 4. Contribution to Our Research Question

Our main research question focuses on identifying different bicycle rental patterns based on trip duration, distance, and rental time.

Weather conditions may help explain why these patterns occur. For example, rainfall or strong winds may be associated with shorter bicycle trips, while comfortable temperatures may be associated with longer trips.

By comparing weather conditions across the identified clusters, we hope to understand whether environmental factors are related to different bicycle usage patterns.

This additional information could make our clustering results easier to interpret.

## 5. Connection to Our Primary Dataset

Our primary dataset contains bicycle rental timestamps, while the supplementary dataset provides hourly weather observations.

We plan to connect the two datasets using their date and hour information. First, we will extract the rental date and hour from rental_datetime. Next, we will prepare the weather observations for the corresponding date and hour.

The datasets could then be joined using these shared time variables. Each bicycle rental record would be associated with weather observations from the corresponding hour.

Before merging, we will check date formats, time zones, missing values, and duplicate weather records.

Since the weather observations represent conditions at specific stations, we will also consider the limitations of using a Seoul observation station to represent conditions across the entire city.

## 6. Planned Use in Our Analysis

At this stage, we plan to use the supplementary weather data mainly to provide context for interpreting the clusters.

After identifying groups of bicycle rental trips, we can compare temperature, precipitation, wind speed, and humidity across those groups.

We may also consider weather variables as additional predictors in the classification stage if they help explain cluster membership.

Actual data integration and analysis have not yet been completed. For Session 1, our goal is to identify a suitable supplementary dataset and explain how it could support our research.

## 7. Conclusion

We selected hourly weather observation data because it can provide useful environmental context for Seoul's public bicycle rental patterns.

Combining bicycle rental information with weather observations may help us better understand the characteristics of different rental groups and make our clustering results more meaningful.
