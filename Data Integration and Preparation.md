# Part 1: Data Integration and Preparation

## 1. Data Sources

Our primary dataset contains Seoul's public bicycle rental records from January to June 2026. It includes 18,511,943 rental records.

Daily weather observations from KMA weather station 108 are used as supplementary data. Station location data and the English station lookup are also used to validate station identifiers.

## 2. Data Integration

Individual rental records were aggregated by station ID and date. The daily rental counts were then combined with weather observations using the date as the merge key.

A many-to-one merge was used because multiple bike stations share the same daily weather observations.

The station-level features summarize rental behavior over the six-month study period.

## 3. Data Validation

### Weather Data

- Total observations: 181
- Duplicate dates: 0
- Missing dates: 0
- Missing values after preprocessing: 0

The weather dataset covers the entire study period.

### Station Location Data

- Total station records: 3,430
- Unique station IDs: 3,430
- Duplicate station IDs: 0
- Missing station IDs: 0
- Invalid coordinates: 77

Stations with invalid coordinates should be excluded from future spatial analysis.

### Integration Results

| Validation | Before Integration | After Integration |
|---|---:|---:|
| Station-date observations | 492,721 | 492,721 |
| Total rentals | 18,511,943 | 18,511,943 |

No duplicate station-date pairs or unmatched weather records were found. The integration preserved all rental counts in the aggregated dataset.

## 4. Final Station-Level Dataset

The station-level dataset contains 2,807 stations and 17 columns.

All 2,807 station IDs match the location dataset. However, 46 stations are missing from the English station lookup. These stations are retained because station names are not required for PCA.

Thirty stations with fewer than 50 rentals were excluded from PCA to reduce the influence of stations with limited activity.

## 5. PCA Data Preparation

The final PCA input contains 2,777 stations and 10 behavioral variables.

| Selected Variable | Description |
|---|---|
| am_peak_share | Morning peak rental share |
| pm_peak_share | Evening peak rental share |
| night_share | Nighttime rental share |
| weekend_share | Weekend rental share |
| median_duration_min | Median trip duration |
| round_trip_share | Round-trip rental share |
| am_net_flow | Morning net flow |
| pm_net_flow | Evening net flow |
| log_total_rentals | Log-transformed rental volume |
| non_member_share | Non-member rental share |

No missing or infinite values remain in the selected variables.

Median trip distance was excluded because of its strong correlation with trip duration. Station identifiers, weather-related variables, and spatial variables were also excluded from PCA.

The selected variables are clipped at the 1st and 99th percentiles and standardized using StandardScaler. This reduces the influence of extreme values and allows variables with different measurement scales to be compared.

## 6. Limitations

Weather observations come from a single weather station and may not represent local conditions at every bike station.

Weather-related variables are excluded from PCA because seasonal patterns may influence their relationship with rental demand.

Spatial and weather-related information will be used in later stages to help explain differences between station profiles.
