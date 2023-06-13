---
jupytext:
  cell_metadata_filter: -all
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.5
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# End-to-End workflow

## EDA

### Python

- `lambda <arguments> : <Return Value if condition is True> if <condition> else <Return Value if condition is False>`

### Descriptive statistics of data

- getting dimensions of df `df.shape`
- show first 5 df `df.head()` or last 5 rows of `df.tail()`
- getting column names and dtypes and more `df.info()`
- check for how many are 
  - numerical `df.select_dtypes(include=['int64','float64'])` and 
  - categorical `df.select_dtypes(exclude=['int64','float64'])`
- getting stats info like mean, std distribution of NUMERIC VARs `df.describe()`
- check for total of NULL cells `df.isnull().sum()`
- check dist of named column `df.groupby(TARGET).size()`
- check no of unique values for an attribute> `df.ATTRIBUTE.unique()`
- check dist of an attribute's values `df.ATTRIBUTE.value_counts()`
- check for variance `df.var()`
- check for missing:
  - show only the column names with missing data `df.columns[df.isnull().any()]`
  - show only the missing columns with number of missing `df[df.columns[df.isnull().any()]].isnull().sum()`
  - pct of missing against total `df[df.columns[df.isnull().any()]].isnull().sum() * 100 / df.shape[0]`

+++

### Basic visualizations

- plot boxplots of VARs in 2x2 subplot `df.plot(kind='box', subplots=True, layout=(2,2), sharex=False, sharey=False)`
- plot histogram `df.hist()`
- plot pairwise x-vs-y for all VARs in a scatter plot `scatter_matrix(df)`
- ydata-profiling
```python
from ydata_profiling import ProfileReport

profile = ProfileReport(df, title="Profiling Report")
profile.to_notebook_iframe()
```

## Preprocessing

Preprocessing is the overall group of performing

- **data cleaning**
  - missing data, correcting data, correcting data structures
- **data scaling**/normalization/standardization
- **feature engineering** : label encoding or OHE or derived features like creating `def get_age()` module
- **dealing with skewed** / long-tail columns, take the log of log(x+1): `np.log1p(df.col)`
- strategies of **dealing with outliers** :
  - apply mean(), the average value
  - apply mode(), the most frequent value
  - apply a constant value
  - for time-series, apply `ffill` or `bfill`

### Ways of dealing with MISSING data

- remove row-wise (not recommended) `df.dropna()`
- remove columns-wise column VARs `df.drop([VARs], axis=1)`
- remove filtered out rows with missing cells ```df.dropna(subset=["COL-NAMEs"], thresh=#)``` with # min of non-missing values
- missingno library `msno.matrix(df)` after importing it `import missingno as msno`
- also used by pandas-profiling/ydata-profiling
- data-wrangler also shows missins data information 

### Cleaning data

- for binary classification problems, convert to `int` datatype `df[VAR].astype(int)` eg: `df.Loan_Status = (df.Loan_Status == 'Y').astype(int)`
- then can check for percentage of distribution with `df.Loan_Status.mean()` as all YESes are 1s, the mean is the % of YESes against total rows
- these applies to both cell data and column names
  - encode all to lowercase `str.lower()`
  - remove spaces `str.replace(' ', '')` or replace with `_` `str.replace(' ', '_')` or remove the `_` all depends on the dataset
- [rebin](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.cut.html) if categorical range of numbers, or categorical dtypes makes more sense than continuous numbers: `pd.cut()`. can be applied to Age or income if too many outliers or long-tail and too valuable to drop

+++

### Imbalanced data

- Use stratified sampling to split up the dataset according to the y dataset
`X_train, X_test, y_train, y_test = train_test_split(X, y, stratify=y, random_state=42)`

### Standardization and Scaling

#### What is it?

`Standardization`: process to make continous (numerical) data _appear normally distributed_ ie the bell shape

`Scaling`: process to make range similar and not have high variance

#### When is it necessary?

`Standardization`: when using models that relies on _linear_ space and distance of datapoints is an important factor

`Scaling`: when 
1. data have _high_ variance (many outliers)
1. data have different scales like `bedrooms`=1 and `price`=500000
1. linearity is a feature of the model's algorithm

- standardize with log normalization `np.log(df[VAR])`
- scale with StandardScaler
```
# Import StandardScaler
from sklearn.preprocessing import StandardScaler

# Create the scaler
scaler = StandardScaler()

# Subset the DataFrame you want to scale 
wine_subset = wine[['Ash', 'Alcalinity of ash', 'Magnesium']]

# Apply the scaler to wine_subset
wine_subset_scaled = scaler.fit_transform(wine_subset)
```

## Feature Engineering

### Categorical
- use DictVectorizer : 

- use sklearn's `LabelEncoder` :
be aware of the inherent "order" if converting categoricals to Ints. If var is like low/med/high than it's fine; but not for fruit-types or housing-types for example

```{code-cell}
enc = LabelEncoder()
hiking['Accessible_enc'] = enc.fit_transform(hiking['Accessible'])
```

* declaring them as categorical instead of `int` or `object` : 
`df.attr.astype("category")`

### Numerical

- Use .loc to aggregate a mean column

```{code-cell}
running_times_5k["mean"] = running_times_5k.loc[:,"run1":"run5"].mean(axis=1)
```

### Dates
- convert to `datetime` and extract date components

```{code-cell}
volunteer["start_date_converted"] = pd.to_datetime(volunteer['start_date_date'])
volunteer["start_date_month"] = volunteer['start_date_converted'].dt.month
```

### Combining with other datasets

From /mnt/z/MEGA/AISG/aiap-1-Professionals/Foundations in AI/AI4I-2 Libraries and Data Manipulation/LIB-4 Merging DataFrames with pandas
* inner join `taxi_owners.merge(taxi_veh, on='vid', suffixes=('_own','_veh'))`
* concat `tracks_from_albums = pd.concat([tracks_master, tracks_ride, tracks_st], sort=True)`
* merge_ordered `gdp_pop = pd.merge_ordered(gdp, pop, on=['country','date'], fill_method='ffill')`
* merge_asof gdp_recession = pd.merge_asof(gdp, recession, on='date')``
* melt `bond_perc = ten_yr.melt(id_vars='metric', var_name='date', value_name='close')`

## Feature Selection

How to identify areas for Feature Selection?
Dependingon the problem statement,

- redundant features that have been encoded into other features
- highly correlated features 
  - eg city, state & Lat, Lon. Choose one pair not both. or drop all except State if we only need such high-level overview ie if Problem statement do not require pinpoint location, Lat & Long are redundant
  - eg moves together directionally in .corr() using Pearson's
- duplicates eg extracted content, or summarized content - remove the original
- 

## Modelling

### Model Selection

### Training

### Evaluation

## MLOps

### Experimentations
