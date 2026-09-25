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

### Model 1:

1. **Data Cleaning:**

     Filtered dataset to non-null entries of Adult weight and Maximum longevity, under Class Mammalia. 
     Removed entries with questionable Data quality as well.

    *Final cleaned dataset contained 996 entries*

2. **Splitting and Log - Transformation:**

    Data was Train-Test split, stratified by 'Order'. Train and test data was then log- transformed to obtain the linear relationship between X and y required to build the model.

3. **Building the Pipeline :**

    Pipeline was built to scale and fit the data to the Huber Regressor model.

4. **Residual Calculation and Model Evaluation:**

    Residuals and Evaluation metrics calculated. Train and test set residuals appended to train and test datasets.

### Model 2:

 1. **Data cleaning:**

    Datasets filtered to non- null entries of Metabolic rate, as it is  presumed to be an important predictor of lifespan, according to the Rate of Living theory. With only 342 non-null values, imputation would mean heavy distortion of the data. Other columns with extensive nulls were removed as well.

 2. **Feature Engineering:**

    Mass-specific BMR for each entry was calculated by dividing Metabolic rate by Body mass. This was done to reduce the effect of Body mass on Metabolic rate, in order to get a better evaluation of the true relation between Metabolic rate and longevity.

3. **Imputation :**

   Remaining null values were imputed in a sequential manner with a custom 'Taxonomical Imputer'. It calculated the median feature value for each genus, family and order of the dataset as well as an overall feature median. Each null was imputed with its corresponding genus' median wherever available, falling back to family then order then overall feature median, until no nulls were left.  
   This method was used in an attempt to impute null values with the most biologically related data that was available.

4. 




## 5. Analysis and metrics


---


## 6. Key Findings


---


## 7. Limitations and Future Enhancements

---


## 8. Requirements