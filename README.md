# Air Pollution and Asthma Burden in Indian Cities

## Overview

This project began as an exploratory attempt to understand the relationship between **air pollution levels and asthma burden across Indian regions**.
Air pollution is widely recognized as a major contributor to respiratory diseases. 
The goal of this project was to investigate whether publicly available datasets could reveal correlations between **Air Quality Index (AQI) metrics and asthma prevalence**.

During the process, the project evolved into an exploration of **data quality, missing data mechanisms, and the challenges of working with public health datasets in India**.

---

## Objectives

The initial objectives were:

- Perform **exploratory data analysis (EDA)** on AQI data across Indian cities.
- Compare pollution patterns with **asthma prevalence data**.
- Identify potential relationships between:
  - Different pollutants and asthma burden
  - Seasonal pollution patterns
  - Cities with significant air quality fluctuations
  - Regional differences in respiratory illness prevalence

---

## Data Sources

The project relied on publicly available datasets:

- Air Quality Index (AQI) data across Indian cities (via Kaggle)
- Government-reported health statistics on asthma prevalence (via data.gov.in)

However, two major limitations emerged during data collection:

1. **Limited availability of granular health datasets in India**
2. **Significant missing values in AQI datasets**

The asthma dataset that was obtained contained **only two years of summarized data at the state level**, which makes it statistically insufficient for meaningful correlation analysis.

---

## Data Quality Challenges

While examining the AQI dataset, a large number of **missing values** were identified.

To properly address this, I explored the statistical foundations of missing data and studied different types of missingness:

- **MCAR (Missing Completely At Random)**
- **MAR (Missing At Random)**
- **MNAR (Missing Not At Random)**

Understanding these categories was important to avoid:

- Shifting the **mean of the dataset**
- Altering the **distribution**
- Introducing **bias through inappropriate imputation**

This led to experimentation with different techniques for handling missing data across:

- Numeric variables
- Categorical variables
- Time series data

Dummy datasets for all the cases and several visualizations were created to inspect patterns in missing values and assess suitable imputation strategies.

---

## Current Status

So far, the following steps have been completed:

- Initial **data collection and cleaning**
- Identification and analysis of **missing values**
- Preliminary **aggregation of AQI data**

These steps are documented in the accompanying **Jupyter Notebook**.

However, further correlation analysis between AQI and asthma burden was not pursued because the available health dataset contains only two data points (two years of summary statistics). 
Drawing statistical conclusions from such limited data would be unreliable.
Continuing the analysis in this situation would likely fall into the **sunk cost fallacy**, where effort is invested despite insufficient data to support meaningful conclusions.

---

## Potential Research Directions (With Better Data)

If more granular health datasets were available, several meaningful analyses could be performed:

- Impact of specific pollutants (PM2.5, PM10, NO₂, SO₂) on asthma prevalence
- Seasonal variation in pollution and respiratory illness
- Identification of cities with sharp air quality fluctuations
- Comparison of urban vs rural respiratory disease patterns
- Relationship between healthcare infrastructure availability and disease burden
- Analysis of government investment in healthcare infrastructure in polluted regions

Such datasets could enable more rigorous statistical modeling and potentially inform public health policy discussions.

---

## Key Takeaways

This project highlighted several important lessons:

- **Public health datasets are often fragmented and difficult to access (in Indian context)**
- **Data quality assessment is as important as analysis**
- Understanding **missing data mechanisms** is critical before applying imputation techniques
- Statistical inference requires **sufficient data resolution and sample size**
- Choosing the right datasets early is crucial, as data availability and granularity determine the scope of analysis

Although the project did not progress to full correlation analysis, it provided valuable insight into the **practical challenges of working with real-world environmental and healthcare data**.