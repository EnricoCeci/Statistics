# Texas Real Estate Market Analysis

---

## Overview

This project consists of a descriptive statistical analysis developed in R to examine historical trends in the Texas real estate market and support data-driven decisions related to property sales and real estate listings.

The analysis combines descriptive statistics, probability calculations, derived indicators, conditional analysis and data visualisation to investigate market behaviour across cities, years and months.

The project focuses on:

- descriptive statistical analysis of the dataset, including variable classification, measures of location, variability, shape and frequency distributions;
- derivation and evaluation of additional indicators, including mean property price, listing effectiveness and selected probability measures;
- conditional analyses by city, year and month using summary statistics;
- visual interpretation of temporal and spatial market patterns through boxplots, bar charts and line charts.

The project was developed following a predefined statistical analysis specification, with particular attention to the interpretation of results rather than to programming complexity.

---

## Technologies

- R
- Base R
- dplyr
- ggplot2
- knitr
- moments
- tidyr
- Google Colab

---

## Project Requirements

### Texas Real Estate Market Analysis

The objective of the project is to analyse historical real estate sales data for Texas Realty Insights and provide statistical and visual insights that can support sales strategy and listing optimisation.

The project includes the following tasks:

- Identify and classify the statistical variables in the dataset.
- Evaluate the treatment of variables with a temporal dimension.
- Calculate measures of location, variability and shape where statistically appropriate.
- Analyse frequency distributions for variables for which these measures are not meaningful.
- Identify the variables with the highest variability and skewness.
- Group a quantitative variable into classes and construct a frequency distribution.
- Calculate and interpret the Gini heterogeneity index.
- Calculate selected probabilities from the dataset.
- Create a mean property price variable using the available information.
- Develop an indicator of listing effectiveness.
- Perform conditional statistical analyses by city, year and month.
- Calculate conditional means and standard deviations.
- Visualise price distributions, sales volumes and historical sales trends using `ggplot2`.
- Compare cities and time periods and provide statistical comments on the results.
- Summarise the main temporal and spatial patterns observed in the Texas real estate market.

---

## Dataset

The project uses the `realestate_texas.csv` dataset, which contains **240 monthly observations** covering four Texas cities over the period **2010-2014**.

Each city is observed for all twelve months of each year, resulting in:

- 4 cities;
- 5 years;
- 12 months per year;
- 60 observations per city;
- 240 observations in total.

The dataset contains the following variables:

- `city` — reference city;
- `year` — reference year;
- `month` — reference month;
- `sales` — total number of sales;
- `volume` — total sales value, expressed in millions of dollars;
- `median_price` — median sale price, expressed in dollars;
- `listings` — total number of active listings;
- `months_inventory` — estimated number of months required to sell the available inventory at the current sales rate.

Dataset source:

[Real Estate Texas dataset](https://drive.google.com/file/d/1O4If8876MTwstkrZX0BqpQ_BxcsIMEko/view?usp=sharing)

The notebook downloads the dataset from Google Drive and imports it directly into the R environment.

---

## Methodology

The project includes the following stages:

- Dataset import and inspection.
- Classification of variables as qualitative or quantitative and discussion of their measurement properties.
- Descriptive statistical analysis of the quantitative variables using:
  - minimum and maximum;
  - quartiles;
  - mean;
  - median;
  - interquartile range;
  - variance;
  - standard deviation;
  - coefficient of variation;
  - skewness;
  - kurtosis.
- Density plots for the continuous variables.
- Comparison of coefficients of variation to identify the variable with the highest relative variability.
- Comparison of skewness coefficients to identify the most asymmetric distribution.
- Discretisation of `sales` into classes.
- Construction of absolute, relative and cumulative frequency distributions.
- Calculation of the normalised Gini heterogeneity index for the grouped `sales` variable.
- Probability calculations based on city, month and year-month combinations.
- Creation of the derived variable `mean_price`:

  `mean_price = volume × 1,000,000 / sales`

- Creation of the derived indicator `current_sales_speed`:

  `current_sales_speed = listings / months_inventory`

- Calculation of average listing clearance rates by city.
- Conditional analysis of `sales` and `listings` by:
  - city;
  - year;
  - month.
- Calculation and graphical representation of conditional means and standard deviations.
- Boxplot analysis of:
  - median prices by city and year;
  - sales volume by city;
  - sales volume by year.
- Bar chart analysis of:
  - total sales volume by month;
  - total sales volume by city;
  - monthly sales by city;
  - normalised monthly sales shares.
- Line chart analysis of:
  - total annual sales;
  - sales over time by city;
  - annual sales comparisons across cities.
- Final interpretation of the market from both temporal and spatial perspectives.

---

## Project Structure

```text
1. Texas RE Mkt Analysis/
│
├── README.md
├── .gitignore
└── Texas_Real_Estate_Market_Analysis.ipynb
```

The dataset is not stored in the repository because it is downloaded directly from Google Drive by the notebook.

---

## Main Findings

The descriptive analysis shows that:

- `volume` is the variable with the highest relative variability, with a coefficient of variation of approximately **53.7%**.
- `volume` is also the most positively skewed variable, with a skewness coefficient of approximately **0.88**.
- After grouping `sales` into classes, the normalised Gini heterogeneity index is approximately **0.928**, indicating a distribution close to maximum heterogeneity across the defined classes.
- The probability that a randomly selected observation refers to Beaumont is **25%**.
- The probability that a randomly selected observation refers to July is approximately **8.3%**.
- The probability that a randomly selected observation refers to December 2012 is approximately **1.7%**.


The derived price analysis shows that:

- Bryan-College Station has the highest average property price, approximately **$183,534**.
- Tyler follows with an average price of approximately **$167,677**.
- Beaumont has an average price of approximately **$146,640**.
- Wichita Falls has the lowest average price, approximately **$119,430**.


The listing effectiveness indicator shows that the average estimated monthly listing clearance rate is:

- approximately **261 listings per month** for Tyler;
- approximately **200 listings per month** for Bryan-College Station;
- approximately **172 listings per month** for Beaumont;
- approximately **117 listings per month** for Wichita Falls.

Tyler therefore records the highest average listing clearance rate, while Wichita Falls records the lowest.


The conditional analysis shows that:

- Tyler has the highest average number of both sales and active listings.
- Wichita Falls has the lowest average number of sales and active listings.
- Across cities, average listings and average sales generally move in the same direction, with Bryan-College Station as the main exception.
- Across years, the average number of sales decreases from 2010 to 2011 and then increases from 2012 onward.
- Across months, sales activity is generally stronger during the central part of the year.


The visual analysis further indicates that:

- Bryan-College Station records the highest median and mean prices.
- Tyler records the highest overall sales activity and sales volume despite lower prices than Bryan-College Station.
- Sales activity is particularly strong between approximately March and August for Tyler and especially Bryan-College Station.
- Tyler maintains relatively high sales levels even after August.
- Wichita Falls shows a comparatively stable but lower level of activity over time.
- Beaumont generally follows market patterns similar to Tyler and Bryan-College Station, but at a lower level.


Overall, the analysis suggests two main dimensions of the Texas real estate market:

- a **temporal dimension**, characterised by a decline in activity between 2010 and 2011, subsequent growth from 2012 onward and stronger activity during the middle months of the year;
- a **spatial dimension**, characterised by Tyler as the strongest market in terms of sales activity and volume, Bryan-College Station as the highest-priced market, and Beaumont and Wichita Falls as the lower-performing markets in the dataset.

These findings describe statistical associations and observed market patterns and should not be interpreted as causal relationships.

---

## Statistical Interpretation

The project is primarily a statistical analysis rather than a programming exercise.

Particular attention is therefore given to the interpretation of descriptive measures and visual patterns:

- the coefficient of variation is used to compare relative variability across variables measured on different scales;
- skewness is used to evaluate distributional asymmetry;
- the Gini heterogeneity index is applied to the grouped quantitative variable rather than directly to the original continuous measurements;
- conditional means and standard deviations are used to compare sales and listing behaviour across cities, years and months;
- boxplots are used to assess differences in central tendency, dispersion and asymmetry;
- bar charts and line charts are used to identify seasonal, historical and geographical patterns.

The results provide a descriptive representation of the observed data. Relationships between variables are interpreted as statistical associations and do not establish causal effects.

---

## How to Run

The notebook is designed to run in **Google Colab using R**.

Open:

```text
Texas_Real_Estate_Market_Analysis_EN.ipynb
```

Make sure the notebook is running with an R runtime.

If the `moments` package is not already available in the runtime, install it with:

```r
if (!requireNamespace("moments", quietly = TRUE)) {
  install.packages("moments")
}
```

The main libraries used by the project are:

```r
library(dplyr)
library(ggplot2)
library(knitr)
library(moments)
library(tidyr)
```

Then run the notebook cells in order.

The notebook automatically performs:

- dataset download and import;
- dataset inspection;
- variable classification;
- descriptive statistical analysis;
- variability and skewness analysis;
- frequency distribution and Gini index calculation;
- probability calculations;
- creation of derived variables;
- conditional analysis by city, year and month;
- statistical visualisation with `ggplot2`;
- temporal and spatial comparison of the Texas real estate market;
- interpretation and summary of the main findings.
