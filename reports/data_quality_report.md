### Dataset Dimensions

- Observations: 52
- Total columns: 27
- Explanatory variables: 24
- Target variable: `price`
- Additional identifier/metadata columns: `id`, `link`

## Dataset Structure

### Observational Unit

Each row represents one used-car observation/listing.

Therefore:

> 1 row = 1 used car

The target variable is `price`, while the remaining vehicle-related variables
serve as potential explanatory variables.

## Variable Classification

| Category | Variables |
|---|---|
| Target | `price` |
| Categorical predictors | `brand`, `model`, `wheel_drive`, `engine_type` |
| Numerical predictors | `year`, `miles`, `city_mileage`, `highway_mileage`, `horsepower`, `torque`, `engine_capacity_litre`, `fuel_capacity`, `num_cylinder`, `num_owners`, `speed_levels`, `front_headroom`, `front_legroom`, `rear_headroom`, `rear_legroom`, `service_records` |
| Identifier | `id` |
| Metadata | `link` |
| Constant features | `num_seat`, `doors`, `type` |
| Severely incomplete feature | `condition` |

### Note on Variable Types

Variable classification was based on the semantic meaning of the variables,
not solely on their pandas storage dtype.

For example, `wheel_drive` is stored as `int64`, but its values represent
drivetrain categories and are therefore treated as categorical rather than
continuous numerical data.

### Dataset Size

The dataset initially contains 52 observations and 27 columns.

### ID Investigation (id.describe())

The `id` column contains 52 observations with values ranging from 3 to 57.

INTERPRETATION:
A statistical summary was initially examined, but measures such as mean and
standard deviation were not considered meaningful for modeling because `id`
functions as an identifier rather than a measurable vehicle characteristic.

The number of unique IDs was found to be 52, equal to the number of
observations. Therefore, each observation has a unique identifier.

The IDs are not perfectly sequential, suggesting that the dataset may
represent a subset of a larger collection of listings. This does not affect
the modeling process because the ID is not a vehicle characteristic.

### Missing Values

| Variable | Missing Values | Missing Percentage |
|---|---:|---:|
| `condition` | 51 | 98.08% |
| `speed_levels` | 1 | 1.92% |
| All other variables | 0 | 0% |

INTERPRETATION:
`condition` contains 51 missing values out of 52 observations (98.08%).
Only one value is observed, making reliable imputation impractical.

`speed_levels` contains only one missing observation (1.92%). Unlike
`condition`, the feature contains sufficient observed information to consider
an appropriate imputation strategy during preprocessing.

### Constant Features

Three variables were found to contain only a single unique value:

| Variable | Value | Frequency |
|---|---|---:|
| `num_seat` | 5 | 52 |
| `doors` | 4 | 52 |
| `type` | sedan | 52 |

INTERPRETATION:
These variables have zero variation within the dataset and therefore cannot
help explain differences in vehicle price. They are candidates for removal
from the predictive feature set.

### `condition`

`condition` contains:

- 51 missing values
- 1 observed value (`4.0`)
- 98.08% missingness

Because almost the entire feature is missing and only one observation is
available, the variable does not provide sufficient information for reliable
imputation.

### Categorical Variables

#### `brand`

The dataset contains six brands:

| Brand | Count |
|---|---:|
| Honda | 23 |
| Volkswagen | 11 |
| Hyundai | 7 |
| Ford | 5 |
| Chevrolet | 3 |
| Subaru | 3 |

#### `model`

The dataset contains 15 distinct models. Several models occur only once,
while Civic is the most frequent model with 14 observations.

#### `engine_type`

Two engine-type categories are present:

| Engine Type | Count |
|---|---:|
| gas | 49 |
| hybrid_gas_electric | 3 |

The variable is categorical and shows substantial class imbalance in this
sample.

#### `wheel_drive`

Although `wheel_drive` is stored as `int64`, its values represent drivetrain
categories rather than a continuous numerical measurement.

Observed values:

| Value | Count |
|---:|---:|
| 2 | 48 |
| 4 | 4 |

Therefore, `wheel_drive` is treated as a binary categorical variable for
modeling purposes.

### Duplicate Investigation

An initial exact-row duplicate check did not identify duplicate records.

However, investigation of the `link` column revealed two observations
sharing the same listing link. Manual inspection confirmed that these two
observations represent the same vehicle.

Therefore, one duplicate observation will be removed during the preprocessing
stage to prevent the same vehicle from being represented more than once.

## Preprocessing Decision Log

| Variable | Issue | Evidence | Planned Action | Reason |
|---|---|---|---|---|
| `id` | Identifier | 52 unique IDs / 52 rows | Exclude | No predictive meaning |
| `link` | Metadata | 51 unique links; duplicate listing identified | Exclude | Source metadata, not a vehicle characteristic |
| `num_seat` | Constant | All values = 5 | Remove | Zero variation |
| `doors` | Constant | All values = 4 | Remove | Zero variation |
| `type` | Constant | All values = sedan | Remove | Zero variation |
| `condition` | Severe missingness | 98.08% missing | Remove | Insufficient observed information |
| `speed_levels` | One missing value | 1.92% missing | Retain + impute | Sufficient observed data |
| Duplicate vehicle | Duplicate observation | Same listing identified | Remove one record | Prevent duplicate representation |
