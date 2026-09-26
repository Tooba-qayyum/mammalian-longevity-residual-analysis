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

    Pipeline built to scale and fit the Huber Regressor to the data.

4. **Residual Calculation and Model Evaluation:**

    Residuals and Evaluation metrics calculated. Train and test set residuals appended to train and test datasets.

### Model 2:

 1. **Data cleaning:**

    Dataset was filtered to non- null entries of Metabolic rate, as it is  presumed to be an important predictor of lifespan, according to the Rate of Living theory. With only 342 non-null values, imputation would mean heavy distortion of the data. Other columns with extensive nulls were removed as well.

    *Cleaned train and test datasets contained 283 and 59 entries, respectively.*

 2. **Feature Engineering:**

    Mass-specific BMR for each entry was calculated by dividing Metabolic rate by Body mass. This was done to reduce the effect of Body mass on Metabolic rate, in order to get a better evaluation of the true relation between Metabolic rate and longevity.

3. **Imputation :**

   Remaining null values were imputed in a sequential manner with a custom 'Taxonomical Imputer'. It calculated the median feature value for each genus, family and order of the dataset as well as an overall feature median.
  
   Each null value was imputed with its corresponding genus' median wherever available, falling back to family then order then overall feature median, until no nulls were left.

   This method was used in order to impute null values with the most biologically related data available in the dataset.

4. **Building a Pipeline :**

    Pipeline built to impute missing values then fit the Random Forest Regressor to the data.

5. **Grid Search CV :**

    Performed GridSearch CV to tune the model to the best parameters.

6. **Model Evaluation and Feature Analysis :**

    Analysed final model 2 metrics and permutation importance results.

### Combined Two - Stage Model:
 
- This step has been performed at the end of the project in order to evaluate the performance of both models together, on the same subset.

- Using the formula, 

```
residual = true value - predicted value

```
True values were compared to the sum of the model 1 predictions and model 2 residuals.

## 5. Analysis and Metrics :

| Metric | Description |
| --- | --- |
| R² score | Measures the proportion of variance in the target variable, explained by the model |
| Mean Absolute Error (MAE) | Measures the average magnitude of errors |
---

* Since log-transformed values have been used, MAE obtained throughout the project is in log units. For easier interpretability, an error factor has also been calculated.

```
Error factor = 10^MAE

An error factor of 1.2 would mean predictions typically lie within a factor of 1.2 of true values.

```

* Permutation importance was also analysed at the end of model 2. This measures how important a feature was for the Random Forest Regressor to make its predictions. In Model 2, a higher mean importance value indicates a higher R² score drop, when that feature was shuffled.


---

## 6. Key Findings

### Model 1 :
  
- Test set R² score: 0.565
- Test set MAE: 0.183
- Error factor: 1.52

  This suggests that Adult weight of mammals explains around 57% of variation found in their Maximum longevity. Model 2 investigates how much of the remaining variance can be explained by a set of 10 biological traits.

* Furthermore, the regression line obtained by the model, obtained a similar equation to the mammalian allometric equation used by HAGR for the AnAge database.  

```
Model 1 regression line :

log₁₀(longevity) = 0.661 + 0.159 × log₁₀(adult weight)

HAGR mammalian allometric equation:

tmax = 4.88 * M^0.153
i.e, log₁₀(tmax) = 0.688 + 0.153*log₁₀(M)

```

### Model 2:
 
 - Test set R² Score : 0.445
 - Test set MAE: 0.128
 - Error factor : 1.34 

   This means that for the subset of model 1 that was tested, model 2 was able to account for nearly 45% of the remaining variation in Maximum longevity. 

 * Permutation importance results identified Gestation length with a mean importance score of 0.15 ± 0.08, and Birth weight with a score of 0.08 ± 0.02, to be the features with the largest mean reductions in test set R², when shuffled. Other features' mean importance values are indistinguishable from 0.

 * Gestation length and Birth weight are traits related to parental investment. This suggests that parental - investment related traits may be relevant to predicting maximum longevity of mammals in this dataset. Though, due to the limited scope of this subset, this finding should not be generalised.




---


## 7. Limitations and Future Enhancements

---


## 8. Requirements