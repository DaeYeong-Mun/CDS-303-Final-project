# Variable Selection

## 1. Variable Selection Table

The following table summarizes the 16 variables in our Seoul Public Bicycle Rental History dataset and their proposed roles in the analysis.

| Variable | Description and Unit | Data Type | Proposed Role | Rationale and Preparation |
|---|---|---|---|---|
| bike_id | Bicycle identifier | Categorical | Exclude | Identifier, not useful for clustering |
| rental_datetime | Rental date and time | Datetime | Clustering input (derived) | Extract rental hour and day of week |
| rental_station_number | Starting station code | Categorical | Context | Useful for geographic interpretation |
| rental_station_name | Starting station name | Categorical | Exclude | Redundant with station code |
| rental_dock | Starting dock number | Categorical | Exclude | Not relevant to rental patterns |
| return_datetime | Return date and time | Datetime | Context | Check trip duration consistency |
| return_station_number | Ending station code | Categorical | Context | Handle missing values |
| return_station_name | Ending station name | Categorical | Exclude | Redundant with station code |
| return_dock | Ending dock number | Categorical | Exclude | Not relevant to rental patterns |
| usage_duration_min | Trip duration in minutes | Numerical | Clustering input | Scale and check outliers |
| usage_distance_m | Travel distance in meters | Numerical | Clustering input | Scale and check outliers |
| birth_year | Rider birth year | Numerical | Classification candidate | Derive age and handle missing values |
| gender | Rider gender | Categorical | Classification candidate | Encode and handle missing values |
| user_type | User membership category | Categorical | Classification candidate | Encode categories |
| rental_station_id | Starting station ID | Categorical | Exclude | Redundant identifier |
| return_station_id | Ending station ID | Categorical | Exclude | Redundant identifier |

## 2. Variable Selection Rationale

Our research focuses on identifying different bicycle rental patterns based on trip duration, travel distance, and rental time. Therefore, we selected usage_duration_min, usage_distance_m, and features derived from rental_datetime as the main clustering inputs.
Trip duration and distance describe how bicycles are used, while rental hour and day of the week can help distinguish commuting patterns from recreational usage. We plan to extract these time features from rental_datetime before applying clustering.
For classification, we will consider birth_year, gender, and user_type as additional explanatory variables. These variables may help us understand whether different rider characteristics are associated with the clusters.
Some variables, such as bike_id and station names, will not be used directly for clustering because they are identifiers or contain redundant information. However, station information may still be useful when interpreting geographic rental patterns.
Before analysis, we will check missing values, remove or investigate invalid observations, and scale numerical variables. Categorical variables used for classification will also require appropriate encoding.
The cluster labels will be generated during the clustering stage and later used as the target variable for classification. They will not be included as input features.

## 3. Planned Data Preparation

We plan to check missing values and unusual observations before clustering. Numerical variables will be scaled to prevent differences in measurement units from affecting the results. We will also create rental hour and day of week variables from the rental timestamp.
For the classification stage, categorical predictors will be encoded appropriately. The resulting cluster labels will serve as the classification target.

## 4. Connection to Our Research Question

These variables will help us investigate whether bicycle rental trips can be divided into meaningful groups based on duration, distance, and time of use. After clustering, classification will help us identify the characteristics that distinguish the groups.
This approach follows the explainable cluster analysis framework introduced in the assigned papers.
