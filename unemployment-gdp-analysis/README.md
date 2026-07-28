# Unemployment Rate and U.S. Real GDP Growth Analysis

## Project Overview

This project investigates the relationship between the U.S. unemployment rate and real GDP growth using publicly available macroeconomic data from the Federal Reserve Economic Data (FRED) database. The analysis combines exploratory data analysis (EDA), hypothesis testing, and simple linear regression to examine whether unemployment can explain variations in quarterly GDP growth.

This project was completed as part of my machine learning and statistics learning journey to strengthen my skills in data preparation, statistical inference, and regression analysis using Python.

---

## Research Question

**What is the relationship between the U.S. unemployment rate and U.S. real GDP growth?**

---

## Dataset

The analysis uses two economic indicators from the Federal Reserve Economic Data (FRED):

| Series | Description |
|---------|-------------|
| **UNRATE** | U.S. Civilian Unemployment Rate (%) |
| **GDPC1** | Real Gross Domestic Product (Billions of Chained 2017 Dollars, Seasonally Adjusted Annual Rate) |

Data Source:

- Federal Reserve Economic Data (FRED)
  - https://fred.stlouisfed.org/series/UNRATE
  - https://fred.stlouisfed.org/series/GDPC1

---

## Analysis Period

The analysis uses historical quarterly observations after aligning the unemployment and GDP datasets over the common time period available from FRED.

---

## Data Preparation

The following preprocessing steps were performed:

- Retrieved economic data from FRED.
- Converted dates into a common quarterly frequency.
- Calculated quarterly real GDP growth using percentage change.
- Merged unemployment and GDP datasets by observation date.
- Removed missing observations created during GDP growth calculation.
- Created two unemployment groups:
  - High unemployment (≥ 5%)
  - Low unemployment (< 5%)

> **Note:** The 5% unemployment threshold was selected solely for hypothesis-testing practice. It is an assumed cutoff and may be adjusted depending on the research objective, dataset, or economic conditions.

---

## Exploratory Data Analysis

The project includes:

- Distribution of unemployment rate
- Distribution of GDP growth
- Scatter plot of unemployment versus GDP growth
- Time-series visualization
- Group comparison using boxplots

---

## Statistical Analysis

### Welch's Two-Sample t-Test

To compare mean GDP growth under different unemployment conditions:

- **High unemployment:** Unemployment ≥ 5%
- **Low unemployment:** Unemployment < 5%

**Results**

| Statistic | Value |
|-----------|-------|
| t-statistic | **-0.258** |
| p-value | **0.796** |

### Interpretation

Because the p-value (0.796) is much larger than the 0.05 significance level, we **fail to reject the null hypothesis**. The analysis does not provide sufficient statistical evidence that average GDP growth differs between periods of high and low unemployment under the chosen threshold.

---

## Linear Regression Analysis

A simple linear regression model was fitted:

\[
\text{GDP Growth} = \beta_0 + \beta_1(\text{Unemployment Rate})
\]

### Results

| Metric | Value |
|---------|-------|
| Regression coefficient | **-0.116** |
| Test R² | **-0.073** |

### Interpretation

The regression coefficient is negative, indicating that higher unemployment is associated with lower GDP growth. However, the model's test R² is **-0.073**, suggesting that unemployment alone has poor predictive power for quarterly GDP growth. The model performs slightly worse than simply predicting the average GDP growth, indicating that additional macroeconomic variables are required to improve prediction accuracy.

---

## Limitations

Several limitations should be considered when interpreting the results:

- This analysis examines association rather than causation.
- Only one explanatory variable (unemployment rate) is included.
- GDP growth is influenced by many additional macroeconomic factors, including inflation, interest rates, consumer spending, investment, government expenditure, exports, and unexpected economic shocks.
- The 5% unemployment threshold is an assumed cutoff for educational purposes and should not be interpreted as an economic benchmark.
- A simple linear regression cannot capture the complex dynamics of the macroeconomy.

---

## Conclusion

This study found a negative relationship between unemployment and GDP growth, consistent with economic theory. However:

- The Welch's t-test found no statistically significant difference between the two unemployment groups.
- The regression model demonstrated poor predictive performance (Test R² = -0.073).

These findings suggest that unemployment alone is insufficient for accurately predicting quarterly GDP growth. Future work should incorporate multiple macroeconomic indicators and more advanced machine learning models.

---

## Repository Structure

```
unemployment-gdp-analysis/
├── README.md
├── The Relationship Between Unemployment and U.S. Real GDP Growth.ipynb
├── Final Project_ The Relationship Between Unemployment and U.S. Real GDP Growth_V1.7.pdf
├── requirements.txt
├── LICENSE

```

---

## Project Files

- 📒 **Jupyter Notebook**

  `The Relationship Between Unemployment and U.S. Real GDP Growth.ipynb`

- 📄 **Final Report**

  `Final Project_ The Relationship Between Unemployment and U.S. Real GDP Growth_V1.7.pdf`

---

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy
- Scikit-learn
- Jupyter Notebook

---

## Requirements

Install the required packages using:

```bash
pip install -r requirements.txt
```

---

## References

Federal Reserve Bank of St. Louis. FRED Economic Data.

- https://fred.stlouisfed.org/

U.S. Bureau of Economic Analysis.

- https://www.bea.gov/

U.S. Bureau of Labor Statistics.

- https://www.bls.gov/

---

## License

This project is released under the MIT License.

---

## Author

**Yuna Chou**

MBA | Project Management Professional (PMP)

Transitioning into Data Science and Machine Learning

Interested in:

- Machine Learning
- Econometrics
- Digital Twins
- AI for Economic Modeling
- Data Analytics

GitHub:
https://github.com/yunachou05