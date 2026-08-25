# Newborn Weight Prediction Model

## Overview

This project develops and evaluates a multiple linear regression model in R to predict newborn birth weight using clinical and anthropometric variables collected from 2,500 newborns across three hospitals. The analysis combines descriptive and inferential statistics, hypothesis testing, linear regression, nonlinear and interaction effects, model selection, multicollinearity diagnostics, residual analysis, heteroscedasticity-robust inference, influential-observation analysis, and a final practical prediction.

## Technologies

* **R**
* **Jupyter Notebook / Google Colab**
* **Base R** for statistical modelling and visualization
* **knitr** for table formatting
* **moments** for skewness and kurtosis
* **car** for VIF/GVIF and influential-observation diagnostics
* **lmtest** for regression diagnostic tests
* **sandwich** for heteroscedasticity-robust covariance estimation
* **ggpubr** for the balloon plot used in the hospital/delivery-type analysis

## Project Requirements

The project requires:

* an R environment or a Jupyter/Google Colab runtime with an R kernel;
* an internet connection to download the dataset from Google Drive;
* the R packages used in the notebook.

The notebook checks whether the required packages are installed and installs them when necessary.

## Dataset

The dataset contains **2,500 newborn observations** collected from three hospitals.

Dataset source: [neonati.csv – Google Drive](https://drive.google.com/file/d/1ChfwftuOSH-WLIto_1AvV-_sQIksGeTq/view)

The original variable names are kept in Italian throughout the notebook because they correspond directly to the CSV schema:

* `Anni.madre` (**Mother's age**) — age of the mother in years.
* `N.gravidanze` (**Number of pregnancies**) — number of pregnancies experienced by the mother.
* `Fumatrici` (**Maternal smoking status**) — binary indicator: 0 = non-smoker, 1 = smoker.
* `Gestazione` (**Gestational age**) — duration of pregnancy in weeks.
* `Peso` (**Birth weight**) — newborn birth weight in grams; this is the response variable.
* `Lunghezza` (**Newborn length**) — newborn length, measured in millimetres.
* `Cranio` (**Cranial diameter**) — newborn cranial diameter, measured in millimetres.
* `Tipo.parto` (**Delivery type**) — natural or cesarean delivery.
* `Ospedale` (**Hospital**) — hospital where the birth took place (`osp1`, `osp2`, or `osp3`).
* `Sesso` (**Sex**) — newborn sex: male (`M`) or female (`F`).

During the preliminary analysis, two clearly anomalous values (`0` and `1`) were identified in `Anni.madre`. They were treated as data-entry errors and replaced with the mean maternal age calculated after excluding those two observations.

## Methodology

### 1. Descriptive Analysis

The preliminary analysis examines variable distributions and possible anomalies through:

* summary statistics;
* skewness and kurtosis;
* density plots for continuous variables;
* frequency distributions for discrete variables;
* boxplots and conditional descriptive statistics.

### 2. Hypothesis Testing

Three hypotheses are investigated:

1. **Delivery type and hospital** — a Chi-square test is used to assess whether the frequency of cesarean versus natural deliveries differs significantly across the three hospitals.
2. **Sample versus population means** — one-sample t-tests compare the sample mean of `Lunghezza` and `Peso` with external population reference values.
3. **Anthropometric differences by sex** — two-sample t-tests evaluate whether mean `Peso`, `Lunghezza`, and `Cranio` differ significantly between males and females.

### 3. Regression Model Development

A sequence of multiple linear regression models is estimated:

* **Model 1** includes `Anni.madre`, `N.gravidanze`, `Fumatrici`, `Gestazione`, `Lunghezza`, `Cranio`, and `Sesso`.
* **Model 2** removes the non-significant variables `Anni.madre` and `Fumatrici`.
* **Model 3** adds a quadratic term for `Gestazione`.
* **Model 4** centers `Gestazione` and includes both its centered linear and quadratic components, preserving the principle of marginality while reducing structural multicollinearity.
* **Model 5** introduces the `Gestazione × Lunghezza` interaction.
* **Model 6** introduces the `Gestazione × Cranio` interaction.
* **Model 7** introduces the `Lunghezza × Cranio` interaction.

### 4. Model Selection

The candidate models are compared using:

* adjusted R²;
* Bayesian Information Criterion (BIC);
* VIF for standard linear/quadratic specifications;
* GVIF adjusted for degrees of freedom for models containing interaction terms.

Although the interaction model between `Gestazione` and `Cranio` achieves the highest adjusted R² and is favoured by BIC, **Model 2** is selected as the final model because it provides a very similar explanatory performance with a simpler and more interpretable specification.

### 5. Model Diagnostics

The final model is evaluated through:

* adjusted R² and in-sample RMSE;
* Residuals vs Fitted, Q-Q, Scale-Location, and Residuals vs Leverage plots;
* Shapiro-Wilk test for residual normality;
* Breusch-Pagan test for homoscedasticity;
* HC3 heteroscedasticity-robust standard errors and robust 95% confidence intervals;
* Durbin-Watson test for residual independence;
* leverage values, studentized residuals, and Cook's distance for influential-observation analysis.

### 6. Prediction

The final model is used to estimate the expected mean birth weight for a female newborn from a mother in her third pregnancy giving birth at 39 weeks of gestation, using the sample means of `Lunghezza` and `Cranio` for the remaining predictors.

## Project Structure

```text
Newborn_Weight_Prediction_Model/
├── README.md
├── .gitignore
└── Newborn_Weight_Prediction_Model.ipynb
```

The dataset is downloaded automatically when the notebook is executed and is therefore not stored in the repository.

## Main Findings

* Hospital 2 records the largest number of cesarean deliveries in the sample, but the Chi-square test does not identify a statistically significant association between hospital and delivery type (`p = 0.58`).
* The sample mean values of both birth weight and newborn length differ significantly from the external population reference values used in the analysis.
* Male newborns have higher mean values of `Peso`, `Lunghezza`, and `Cranio` than female newborns, and the differences in means are statistically significant.
* The strongest observed correlations are between `Peso` and `Lunghezza` (approximately `0.80`) and between `Peso` and `Cranio` (approximately `0.70`).
* The selected final model, **Model 2**, includes `N.gravidanze`, `Gestazione`, `Lunghezza`, `Cranio`, and `Sesso`, with an adjusted R² of approximately **0.7265**.
* The best-performing interaction model reaches an adjusted R² of approximately **0.7301**, so the gain in explanatory power over Model 2 is small.
* Model 2 has an in-sample RMSE of approximately **274 g**, corresponding to about **8.3%** of the sample mean birth weight.
* The Breusch-Pagan test detects heteroscedasticity. HC3 robust standard errors increase the estimated uncertainty for some coefficients, but all regressors remain statistically significant; the robust 95% confidence intervals also exclude zero.
* The Durbin-Watson test does not provide evidence to reject the null hypothesis of residual independence.
* Observation **1551** is identified as the most influential and anomalous observation, with a high Cook's distance and a combination of weight and length values that suggests a possible data-entry error.
* For the example profile considered in the assignment, the final model estimates an expected mean birth weight of approximately **3,271 g**.

## How to Run

1. Download or clone the repository.
2. Open `Newborn_Weight_Prediction_Model.ipynb` in **Google Colab** or another Jupyter environment configured with an **R kernel**.
3. Run the notebook cells from top to bottom.
4. The notebook will:

   * install missing R packages when necessary;
   * download `neonati.csv` automatically from Google Drive;
   * import and preprocess the data;
   * run the statistical analyses, regression models, diagnostics, and final prediction.

No manual dataset download is required.
