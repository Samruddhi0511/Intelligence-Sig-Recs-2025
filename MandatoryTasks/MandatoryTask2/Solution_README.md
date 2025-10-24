# Regression Task: Predicting y from w and x
**Task Link**: https://drive.google.com/drive/folders/1I9jY3mVBnWNIYMqCKo3y02TLP2lySPUt?usp=sharing
## Overview
The objective of this task was to predict the target variable `y` using two features `w` and `x`.  
The dataset is simple with three columns:  

- **w**: feature 1  
- **x**: feature 2  
- **y**: target variable  

---

## Approach

### 1. Data Loading and Exploration
- Loaded the dataset using **pandas**.
- Explored basic statistics and feature distributions.
- Visualized scatter plots to examine correlations between `w`, `x`, and `y`.

### 2. Modeling
Tested multiple models to capture the relationship between inputs and the target since cudnt firgure out the relationship:

| Model               | R² Score   | RMSE      |
|--------------------|------------|-----------|
| Linear Regression   | -0.000454  | 0.710857  |
| Ridge Regression    | -0.000454  | 0.710857  |
| Lasso Regression    | -0.000011  | 0.710699  |
| Random Forest       | 0.728628   | 0.370225  |
| Gradient Boosting   | 0.126094   | 0.664379  |

> Observation: Random Forest performed the best, suggesting a **non-linear relationship** between the features and the target. Linear models failed to capture this.  

---

### 3. Visualization
- Scatter plots of predicted vs actual `y` for each model.
- Random Forest predictions closely followed the actual `y` trend, while linear models struggled.  
- Residual plots showed minimal error spread for Random Forest.

 

---

## Conclusion
- Linear methods fail due to the non-linear nature of the dataset.  
- Random Forest successfully models the complex relationship between `w` and `x` to predict `y`.  
- Understanding the hidden structure of features is key in regression tasks.  

---



