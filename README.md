# Mammalian Longevity - Allometric scaling and Residual Analysis.
*Using allometric scaling to predict maximum longevity of mammalian species, then analysing their residuals in order to ascertain biological traits that contribute to unexpected lifespans.*

---

## Table of Contents




---

## 1. Project Overview

The allometric  equation, Y = aMᵇ is often used to describe the relationship between maximum longevity of mammals, and their size. But, certain mammals live unexpectedly longer or shorter lives than their size predicts. This project used the  HAGR AnAge Dataset to build a Huber Regressor that predicts maximum longevity of mammals from their adult weight. The calculated residuals from a subset of the dataset were then used as the target variable for a Random Forest Regressor, in order to analyse the predictive power of 10 biological features. The analysis found traits associated with parental investment, namely birth weight and gestation length, to be the strongest predictors of such deviation.

---

## 2. Data

The dataset for this project has been obtained from The Animal Ageing and Longevity Database, maintained by HAGR. More information about this dataset can be found here: https://genomics.senescence.info/help.html#anage

* No. of Entries in Dataset = 4645
* No. of Columns = 31

---

## 3. Repository Structure


---


## 4. Workflow

>### Model 1:

1. Data Cleaning:
     Filtered dataset by non-null entries of Adult weight and Maximum longevity, under Class Mammalia. 
    
      Removed entries with questionable Data quality as well.

    *Final cleaned dataset contained 996 entries*

2. Splitting and Log - Transformation:
    Data was Train-Test split,stratified by 'Order'. Train and test data was then log- transformed to obtain the linear relationship between X and y required to build the model.

3. Building the Pipeline :
    Pipeline was built to scale and fit the data to the Huber Regressor model.

       
---


## 5. Analysis and metrics


---


## 6. Key Findings


---


## 7. Limitations and Future Enhancements

---


## 8. Requirements