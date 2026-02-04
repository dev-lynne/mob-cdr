## Overview of my approach

I loaded and analyzed 3 SMS/call/internet activity data (sms-call-internet-mi-2013-11-02.csv, sms-call-internet-mi-2013-11-04.csv, sms-call-internet-mi-2013-11-06.csv). I then combined them. I started by loading and preparing the data, then cleaned the data by handling the missing data by replacing the missing values with the mean. I also added some columns to the dataset for analysis. And finally, I did the analysis and some visualizations.

**Data Source:** [Kaggle - Mobile Phone Activity Dataset](https://www.kaggle.com/datasets/marcodena/mobile-phone-activity)  
**Research Paper:** [Nature Scientific Data](http://go.nature.com/2fcOX5E)

### 1: Loading and exploring the dataset
- **Shape:** 6,564,031 rows × 8 columns
- **Each representing a single hour of activity in one grid cell**
- **Nearly 4 million missing values** to handle

### 2: Handling  Missing Data 
**Strategy:**
- Identified all columns with missing values
- Used mean imputation for activity columns (smsin, smsout, callin, callout, internet)
- Documented the number of records modified
- Verified completeness after imputation

### 3. Feature Engineering
Created aggregate columns
- `total_sms` = smsin + smsout
- `total_calls` = callin + callout
- `total_internet` = internet activity
- `total_activity` = sum of all activities

## Key Decisions

### Decision 1: Handling Missign Values
**Choice:** Mean imputation for all activity columns  
**Justification:**
- Mean preserves the central tendency of the distribution
- More conservative than zero-filling, which would underestimate activity

### Decision 2: Domestic vs International Classification
**Choice:** Italy (country code 39) = Domestic, all others = International  
**Justification:**
- The dataset is from Milan, Italy
- Italy has country code of 39


### Decision 4: Peak Hour Identification
**Choice:** Grid-level peak hours aggregated to find most common  
**Alternative Considered:** Simple overall hourly maximum  
**Justification:**
- More representative of spatial patterns
- Accounts for geographic heterogeneity
- Reveals common behavioral patterns across different areas

## Summary of Findings

- **Total Records of dataset:** 6,564,031
- **Unique Grid Squares (CellID):** 10,000
- **Number of unique country codes:** 302
- **Total missing values:** 21,137,195
- **Missing values**:
    - smsout      5025738
    - callin      4761685
    - callout     3764484
    - internet    3621117
- **Most Common Peak Hour:** 17:00 
- **Lowest Activity Hour:** 4:00 AM 
- **total calls by hour**
    - Mean : 3,671,836.31
    - Median: 4,145,010.33
    - Std : 1,837,423.89
    - Min : 971,110.83
    - Max : 5,801,570.12

**Daytime vs Nighttime total activity (%):**
    - **Daytime Activity:**  73.55%
    - **Nighttime Activity:** ~26.45% 
    - More daytime than nightime activity


**Domestic vs Int'l Calls:**
- Domestic calls: 33.11% 
- International calls: 66.89%
- More international calls than domestic


**Domestic vs Int'l SMS:**
- Domestic SMS: 24.98% 
- International SMS: 75.02%
- **Pattern:** Similar to calls but slightly lower international percentage

- **Incoming/Outgoing Ratio of international calls:** 
  - Ratio > 1: More incoming international calls 

#### Activity Type Correlation
**SMS vs Calls at Grid Level:**
- **Correlation Coefficient:** Strong positive correlation (0.9862)
- Areas with high SMS activity also have high call activity