# Food-Insecurity
Using Lasso and Ridge models to predict food insecurity among seniors living in Iowa.

## Predicting Food Insecurity Among Seniors in Iowa
authors: Riley Schultz, Jason Nguyen, Eric Pfaffenbach, and Anthony Esboldt
---
date: 12/12/2024

## Introduction
This repository contains the code and data required to reproduce the results found when using 2022 CPS data to predict variables FSWROUTY and FSBAL when applied to ACS public data. 
---
**Purpose**: Identifying underserved areas in Iowa based on ACS data  
**Designed use**: Lasso and Ridge modeling is used on the data to make predictions  
**Dataset**:  
- **Current Population Survey (CPS)**: Includes predictor variables (X) and food security outcome variables (Y). Variables FSWROUTY and FSBAL measure food insecurity. CPS data is cleaned and formatted in `clean_cps.R`.
  - **FSWROUTY**: Worry about running out of food.  
  - **FSBAL**: Ability to afford balanced meals.   
- **American Community Survey (ACS)**: Includes demographic and geographic data for Iowa. The ACS dataset is formatted using `ACSCleaning.R` to align with CPS structure for predictions.  

**Goal**: Produce results which may point to areas where seniors have food insecurity outside of the DSM area.

---
## Requirements
To install the required R packages, run the following code in R:

```r
install.packages(c("Haven", "tidyverse", "pROC", "glmnet", "lubridate", "sf",
                   "ggplot2", "ggthemes", "logistf", "tigris", "rmapshaper"))
```


## Data
### Download Data Files
- `spm_pu_2022.sas7bdat`: CPS supplemental poverty measure data for 2022.  
- `cps_00006.csv`: Extracted CPS data file with variables for modeling.  
- `total_iowa_seniors_by_puma.csv`: ACS data containing total senior populations by PUMA in Iowa.  

### R Files
- `clean_cps.R`: Prepares CPS data by cleaning and formatting variables for modeling. This includes converting food security variables (e.g., FSWROUTY, FSBAL) into binary outcomes.  
- `ACSCleaning.R`: Cleans and formats ACS data to align with CPS structure for use in prediction. This ensures compatibility between datasets.  
- `predict_wrouty.R`: Trains Lasso and Ridge regression models for the FSWROUTY variable.  
- `predict_FSBAL.R`: Trains Lasso and Ridge regression models for the FSBAL variable.  
- `ACS_WROUTY.R`: Applies trained FSWROUTY models to ACS data to make predictions.  
- `ACS_BAL.R`: Applies trained FSBAL models to ACS data to make predictions.  

---



# Clean the data
```
## [1] run "clean_cps.R" which you can then look into and see the updated data
## [2] run "ACSCleaning.R" Gives you the best version of ACS to later test your models
```


## Reproduce
```
0. Pick your Variables you wish to predict (WROUTY and BAL are used as examples but others can be implemented easily.

https://cps.ipums.org/cps-action/variables/search This link provides access to the variables and what they mean for you to
decide which are best.

1. Run `predict_wrouty.R` or `predict_FSBAL.R` to run the lasso and ridge regression 
  
The above files each respectivly run the models for training the CPS data and are the first step in making predictions
  
2. Run either `ACS_WROUTY.R` or `ACS_BAL.R` to used the train models to predict on ACS data

Here there will be maps produced in which we see both the population as a whole based on the average weights of proportions who may
struggle in regards to WROUTY or BAL depending on which files you chose to run. The second map is produced to show the seniors only
on the map and suggests how many seniors are struggling in that PUMA. There will also be a data frame called "results" created that
shares the numbers by PUMA id of the amount of predicted seniors. 
