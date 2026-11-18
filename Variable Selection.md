# Variable Selection

Our unit of analysis is the **station**. The raw dataset has one row per **trip**, so most clustering inputs are **derived features**: trip-level variables aggregated for each rental station. The tables below keep the **existing variables** (in the raw file) separate from the **derived station-level features**, which are now built in our notebook (Session 2).

**Roles**
- **Clustering input:** used to form the clusters.
- **Classification input:** used as a predictor when we later classify the cluster labels.
- **Contextual:** used only to describe and interpret clusters after they are formed.
- **Exclude:** not used in modelling.

## 1. Variable Selection Table

### 1.1 Existing variables (raw trip file, 18,511,943 rows)

The following table summarizes the 16 variables in our Seoul Public Bicycle Rental History dataset and their proposed roles in the analysis. Missing-value counts come from our [Bike-S notebook](https://github.com/DaeYeong-Mun/CDS-303-Final-project/blob/main/notebooks/Bike-S.ipynb).

| Variable | Description and Unit | Data Type | Proposed Role | Rationale and Preparation |
|---|---|---|---|---|
| bike_id | Bicycle identifier (e.g. SPB-65030) | Categorical (ID) | Exclude | Identifier, not useful for clustering; 261 missing |
| rental_datetime | Rental date and time | Datetime | Source for derived features | Extract rental hour, day of week, and date (for the weather join) |
| return_datetime | Return date and time | Datetime | Source for derived features | Return hour and weekday time the arrivals used in am_net_flow and pm_net_flow |
| rental_station_id | Starting station ID (e.g. ST-1461) | Categorical (ID) | Grouping key | Defines the unit of analysis and joins to station coordinates; never a model input |
| rental_station_number | Starting station code | Categorical | Exclude | Redundant with station ID |
| rental_station_name | Starting station name | Categorical | Exclude | Redundant with station ID; names can change over time, so we join on IDs |
| rental_dock | Starting dock number | Numeric code | Exclude | Mostly 0; not relevant to rental patterns |
| return_station_id | Ending station ID | Categorical (ID) | Source for derived features | Used for round-trip share and net flow; 100,206 missing (≈0.5%), and those trips are dropped from return-based features |
| return_station_number | Ending station code | Categorical | Exclude | Redundant with return_station_id |
| return_station_name | Ending station name | Categorical | Exclude | Redundant with return_station_id |
| return_dock | Ending dock number | Numeric code | Exclude | Mostly 0; not relevant to rental patterns |
| usage_duration_min | Trip duration in minutes | Numerical | Source for derived features | Strongly skewed (max 65,977 min); trim implausible trips and use station medians |
| usage_distance_m | Travel distance in meters | Numerical | Source for derived features | Strongly skewed (max ≈13.2 million m); same treatment as duration |
| birth_year | Rider birth year | Numerical | Source (optional), or exclude | 465,492 missing or impossible values (0, 2099); if used, keep plausible years and aggregate to a station median rider age |
| gender | Rider gender (M/F) | Categorical | Exclude (contextual at most) | 4,564,501 missing (≈25%), too incomplete to rely on |
| user_type | Domestic / foreign / non-member | Categorical | Source for derived features | No missing values; aggregated to non_member_share, so no one-hot encoding is needed |

### 1.2 Derived features (station level, built in Session 2)

Updated in Session 2 to the features actually computed in the notebook. Changes from the original plan are marked **(changed)**.

| Feature | Description and Unit | Data Type | Proposed Role | Rationale and Preparation |
|---|---|---|---|---|
| total_rentals | Rentals starting at the station, Jan–Jun 2026 (count) | Numerical | Filter | Stations with fewer than 50 rentals are excluded (30 stations) so that ratios are not noisy |
| log_total_rentals | log10(total_rentals) | Numerical | Clustering input | Station size; the log reduces skew before scaling |
| am_peak_share | Share of rentals on weekdays 07:00–09:59 (0–1) | Numerical | Clustering input | Signals commuter (morning) use |
| pm_peak_share | Share of rentals on weekdays 17:00–19:59 (0–1) | Numerical | Clustering input | Signals commuter (evening) use; r = −0.62 with am_peak_share, so both are kept |
| night_share | Share of rentals 22:00–04:59 (0–1) | Numerical | Clustering input | Signals nightlife or late-shift use |
| weekend_share | Share of rentals on Saturday/Sunday (0–1) | Numerical | Clustering input | Signals leisure use |
| median_duration_min | Median trip duration (minutes) | Numerical | Clustering input | The median is robust to implausible trips; clipped at the 1st/99th percentile across stations |
| median_distance_m | Median trip distance (meters) | Numerical | Exclude **(changed)** | r = 0.91 with median_duration_min, so it is dropped to avoid double-counting trip length |
| round_trip_share | Share of trips returned to the same station (0–1) | Numerical | Clustering input | Signals leisure loops |
| am_net_flow, pm_net_flow **(changed)** | (returns − rentals) / (returns + rentals) during weekday 07:00–09:59 and 17:00–19:59, −1 to 1 | Numerical | Clustering input | Replaces a single daily net_flow_ratio: morning outflows and evening inflows cancel out over a day (median ≈ 0), so the daily value hides the commute |
| non_member_share **(changed)** | Share of rentals by non-members (0–1) | Numerical | Clustering input | Signals tourist or occasional use; foreign_share was dropped because it is almost always 0 (median 0.000) |
| rain / cold sensitivity **(changed)** | Response of daily rentals to rain and temperature | Numerical | Contextual (after clustering) | Not used as station-level inputs: linking daily weather to six-month station summaries mixes weather with season and holidays. Instead, each cluster's daily rentals will be modelled against temperature and rain, controlling for month, day of week and public holidays |
| dist_to_subway_m | Distance to the nearest subway station (meters) | Numerical | Classification input / contextual | From station and subway coordinates; stations with (0, 0) coordinates are excluded |
| district | One of Seoul's 25 districts | Categorical | Contextual | Point-in-polygon with district boundaries |
| cluster_label | Cluster assigned by the clustering step | Categorical | Classification target only | Never used as an input feature |

## 2. Variable Selection Rationale

Our research focuses on identifying different station usage patterns based on time of use, trip length, and rider mix. Therefore, we selected features derived from rental_datetime, return_datetime, usage_duration_min, return_station_id, and user_type as the main clustering inputs, after aggregating them for each rental station. In Session 2 these were reduced with PCA to four components (see the [PCA page](PCA.html)).
The shares of rentals in the morning peak, evening peak, night, and weekend can help distinguish commuting stations from recreational ones, while median trip duration and distance describe how bicycles are used from each station. Round-trip share and morning/evening net flow show whether a station is a destination, a starting point, or a place for leisure loops. We plan to extract these features from the trip records before applying clustering.
For classification, we will consider dist_to_subway_m as an additional explanatory variable, alongside the clustering features. Rider characteristics are included through non_member_share. We will not rely on gender because about a quarter of its values are missing, and birth_year will be used only if enough plausible values remain.
Some variables, such as bike_id, station names, and dock numbers, will not be used directly because they are identifiers or contain redundant information. rental_station_id is used only to group trips and to join station coordinates. Station location and district may still be useful when interpreting geographic patterns.
The cluster labels will be generated during the clustering stage and later used as the target variable for classification. They will not be included as input features.

## 3. Planned Data Preparation

We plan to check missing values and unusual observations at the trip level before aggregating. Trips without a return station are dropped from return-based features only, and trips with implausible durations or distances are trimmed. Station-level features should then have no missing values, apart from stations removed by the volume filter or missing coordinates.
All clustering inputs are clipped at their 1st and 99th percentiles to limit outliers, then scaled (mean 0, standard deviation 1) to prevent differences in measurement units from affecting the results. total_rentals is log-transformed first.
user_type becomes numeric shares, so no one-hot encoding is needed, and district is used only for interpretation. We checked correlations among the derived features: duration and distance were nearly identical (r = 0.91), so distance was dropped, and the remaining correlated features were combined with PCA. The final PCA uses 10 variables and keeps 4 components (81% of the variance).

## 4. Connection to Our Research Question

These variables will help us investigate whether rental stations can be divided into meaningful groups based on time of use, trip length, and rider mix. After clustering, classification will help us identify the characteristics that distinguish the groups.
Because the classification step mainly reuses the clustering features, its accuracy and SHAP values describe which features separate the clusters. They do not independently prove that the clusters exist.
This approach follows the explainable cluster analysis framework introduced in the assigned papers.
