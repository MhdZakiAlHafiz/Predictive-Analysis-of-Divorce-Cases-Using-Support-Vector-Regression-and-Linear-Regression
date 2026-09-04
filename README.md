# Divorce Forecasting in Indonesia

### Comparative Regression Analysis Using BPS Demographic Data

A machine learning project for analyzing and forecasting divorce trends across Indonesian provinces using demographic data from **Badan Pusat Statistik (BPS)**.

This project focuses on identifying the dominant factors associated with divorce and benchmarking **Linear Regression** against **Support Vector Regression (SVR)** to determine which model provides better predictive performance for the aggregated provincial dataset.

---

## Project Overview

Divorce is influenced by multiple social and socio-economic factors. This project analyzes divorce data across **34 Indonesian provinces** over the period **2018-2021**.

The analysis combines four years of provincial-level data and applies a complete data science workflow:

```text
Raw BPS Data
     |
     v
Data Cleaning & Standardization
     |
     v
Multi-Year Data Aggregation
     |
     v
Exploratory Data Analysis
     |
     v
Correlation Analysis
     |
     v
Feature Preparation
     |
     +-------------------+
     |                   |
     v                   v
Linear Regression       SVR
     |                   |
     +---------+---------+
               |
               v
       Model Evaluation
               |
               v
       Performance Comparison
```

The primary goal is to evaluate whether a linear or non-linear regression approach is more suitable for predicting the total number of divorces from reported causal factors.

---

## Objectives

### 1. Data Aggregation & Cleaning

Build a reliable preprocessing pipeline to:

* Combine provincial datasets from 2018, 2019, 2020, and 2021.
* Standardize column names and data formats.
* Handle missing values using mean imputation.
* Remove irrelevant summary records such as `Indonesia` and `Catatan`.
* Produce a single clean dataset for downstream analysis.

### 2. Exploratory Data Analysis

Analyze the distribution of divorce causes across provinces and years to identify the most prominent contributing factors.

### 3. Correlation Analysis

Investigate relationships between divorce-related factors using correlation analysis and heatmap visualization.

### 4. Model Benchmarking

Compare two regression approaches:

* Linear Regression
* Support Vector Regression (SVR)

The models are evaluated using:

* R-squared (R2)
* Mean Absolute Error (MAE)

---

## Dataset

### Source

The dataset was collected from:

**Badan Pusat Statistik (BPS) - Statistics Indonesia**

Period:

```text
2018
2019
2020
2021
```

Geographical coverage:

```text
34 Indonesian Provinces
```

The final dataset contains divorce counts categorized by reported causes.

### Features

```text
Zina              -> Adultery
Mabuk             -> Drunkenness
Madat             -> Substance Abuse
Judi              -> Gambling
Tinggalkan_Pihak  -> Abandonment
Penjara            -> Imprisonment
Poligami           -> Polygamy
KDRT               -> Domestic Violence
Cacat              -> Physical Disability
Pertengkaran       -> Continuous Disputes
Kawin_Paksa        -> Forced Marriage
Murtad             -> Apostasy
Ekonomi            -> Economic Issues
```

### Target Variable

```text
Jumlah -> Total Number of Divorces
```

---

## Repository Structure

```text
Divorce-Forecasting-Indonesia/
|
+-- Forecasting_data_perceraian.ipynb
|     Main Jupyter Notebook containing the complete
|     data cleaning, EDA, analysis, and modeling workflow.
|
+-- data_percerai.csv
|     Final cleaned and aggregated dataset used for modeling.
|
+-- Jumlah Perceraian Menurut Provinsi dan Faktor, 2018-2021.csv
|     Raw BPS dataset in CSV format.
|
+-- Jumlah Perceraian Menurut Provinsi dan Faktor, 2018-2021.xlsx
|     Raw BPS dataset in Excel format.
|
+-- README.md
|     Project documentation.
```

---

# Methodology

## 1. Data Preprocessing

The preprocessing stage transforms multiple yearly BPS datasets into a consistent analytical dataset.

### Data Standardization

Original column names were simplified into machine-readable names to improve consistency throughout the analysis.

Example:

```text
Original Data
     |
     v
Rename Columns
     |
     v
Standardize Data Types
     |
     v
Handle Missing Values
     |
     v
Remove Irrelevant Rows
     |
     v
Final Dataset
```

### Missing Value Handling

Missing observations were handled using **mean imputation**.

The calculated mean values were rounded to two decimal places before being used for replacement.

### Data Aggregation

The four yearly datasets were concatenated into a unified DataFrame:

```text
2018 Dataset
      |
2019 Dataset
      |
2020 Dataset
      |
2021 Dataset
      |
      v
Master DataFrame
```

Rows representing national-level summaries or notes, such as:

```text
Indonesia
Catatan
```

were removed because the modeling task focuses on provincial-level observations.

---

# Exploratory Data Analysis

The EDA stage was performed to understand the structure and distribution of the dataset before modeling.

The analysis includes:

* Frequency analysis of divorce causes.
* Distribution analysis across provinces and years.
* Comparison of major divorce-related factors.
* Correlation analysis between features.
* Heatmap visualization.

The analysis indicates that **Continuous Disputes (`Pertengkaran`)** and **Economic Issues (`Ekonomi`)** are among the most prominent factors within the aggregated dataset.

---

# Correlation Analysis

A correlation matrix was generated to investigate relationships between the reported divorce factors and the target variable.

```text
+-----------------------------+
|      Correlation Matrix     |
+-----------------------------+
| Divorce Factors             |
|          |                  |
|          v                  |
| Relationship Analysis       |
|          |                  |
|          v                  |
| Multicollinearity Insights  |
+-----------------------------+
```

This step helps identify:

* Strong relationships between predictors.
* Potential multicollinearity.
* Features associated with total divorce counts.
* Relationships that may influence regression performance.

---

# Machine Learning

Two regression algorithms were selected for comparative benchmarking.

## Linear Regression

Linear Regression was used as the baseline model because the aggregated demographic features showed relatively strong linear relationships with the target variable.

Advantages:

* Simple and interpretable.
* Fast to train.
* Easy to explain to non-technical stakeholders.
* Provides a useful baseline for model comparison.

---

## Support Vector Regression

Support Vector Regression (SVR) was evaluated as a non-linear alternative capable of modeling more complex relationships.

SVR was included to determine whether a more flexible regression approach could improve predictive performance compared with the linear baseline.

---

# Model Evaluation

The models were evaluated using two standard regression metrics.

## R-squared (R2)

R2 measures how much of the variance in the target variable can be explained by the model.

```text
Higher R2
   |
   +--> Better explanatory power
```

## Mean Absolute Error (MAE)

MAE measures the average absolute difference between predicted and actual values.

```text
Lower MAE
   |
   +--> Smaller prediction error
```

---

# Results

The benchmarking produced the following results:

```text
+----------------------+----------+-------------+
| Model                | R2       | MAE         |
+----------------------+----------+-------------+
| Linear Regression    | 0.80     | 2,087.56    |
| Support Vector       | -0.06    | 5,468.08    |
| Regression (SVR)     |          |             |
+----------------------+----------+-------------+
```

### Performance Comparison

```text
R2

Linear Regression  ████████████████  0.80
SVR                ▏                -0.06
```

```text
MAE

Linear Regression  ██████████        2,087.56
SVR                █████████████████ 5,468.08
```

The results show a substantial performance difference between the two approaches.

### Linear Regression

```text
R2  = 0.80
MAE = 2,087.56
```

Linear Regression achieved strong predictive performance and explained approximately **80% of the variance** in the target variable.

### Support Vector Regression

```text
R2  = -0.06
MAE = 5,468.08
```

SVR produced a negative R2 score and substantially higher prediction error, indicating poor generalization under the configuration used in this experiment.

---

# Key Findings

The benchmarking results suggest that **Linear Regression was substantially more effective than SVR** for this dataset.

Key observations:

```text
1. Linear Regression achieved R2 = 0.80.

2. Linear Regression produced an MAE of 2,087.56.

3. SVR achieved a negative R2 of -0.06.

4. SVR produced a considerably higher MAE of 5,468.08.

5. The aggregated demographic features appear to have
   sufficiently strong linear relationships with the target
   variable for Linear Regression to perform effectively.
```

The results demonstrate that a more complex algorithm does not necessarily provide better performance. Model selection should be driven by **data characteristics, validation results, and error analysis**, rather than algorithm complexity alone.

---

# Conclusion

This project demonstrates an end-to-end machine learning workflow for demographic data analysis and regression benchmarking.

The experiment found that **Linear Regression outperformed SVR** on the evaluated dataset, achieving:

```text
R2  : 0.80
MAE : 2,087.56
```

compared with:

```text
R2  : -0.06
MAE : 5,468.08
```

The findings suggest that the relationship between the aggregated divorce-related factors and total divorce counts can be effectively captured using a linear model under the experimental setup used in this project.

The poor SVR performance also highlights the importance of **hyperparameter optimization, feature scaling, kernel selection, and validation strategy** when applying non-linear machine learning models.

---

# Tech Stack

```text
Language
+-- Python

Data Processing
+-- Pandas
+-- NumPy

Machine Learning
+-- Scikit-learn

Data Visualization
+-- Matplotlib
+-- Seaborn

Development Environment
+-- Jupyter Notebook
+-- Google Colab
```

---

# How to Run

## 1. Clone the Repository

```bash
git clone https://github.com/YourUsername/Divorce-Forecasting-Indonesia.git

cd Divorce-Forecasting-Indonesia
```

## 2. Install Dependencies

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

## 3. Launch Jupyter Notebook

```bash
jupyter notebook Forecasting_data_perceraian.ipynb
```

Alternatively, the notebook can be opened using **Google Colab**.

If using Google Colab, update the dataset paths according to the location of the uploaded or mounted files.

---

# Skills Demonstrated

This project demonstrates practical experience in:

```text
Data Analytics
+-- Data Cleaning
+-- Data Transformation
+-- Data Aggregation
+-- Exploratory Data Analysis
+-- Correlation Analysis

Machine Learning
+-- Regression
+-- Linear Regression
+-- Support Vector Regression
+-- Model Benchmarking
+-- Model Evaluation

Python
+-- Pandas
+-- NumPy
+-- Scikit-learn
+-- Matplotlib
+-- Seaborn
```

---

# Future Improvements

Potential improvements for future iterations include:

```text
+ Hyperparameter tuning for SVR
+ Grid Search / Randomized Search
+ Cross-validation
+ Feature scaling optimization
+ Feature selection
+ Polynomial Regression
+ Random Forest Regression
+ Gradient Boosting
+ XGBoost
+ Time-series forecasting approaches
+ Additional socio-economic indicators
+ More recent BPS datasets
```

These improvements could provide a broader benchmark and help determine whether more advanced models can outperform the linear baseline under optimized conditions.

---

# Author

**Muhammad Zaki Al Hafiz**

Data Science | Data Analytics | Machine Learning

```text
Focus Areas
+-- Data Analysis
+-- Predictive Analytics
+-- Machine Learning
+-- AI
```

* LinkedIn: [www.linkedin.com/in/zakialhafiz]
* GitHub: [https://github.com/MhdZakiAlHafiz/Predictive-Analysis-of-Divorce-Cases-Using-Support-Vector-Regression-and-Linear-Regression.git]

---

# License & Data Source

The dataset used in this project was obtained from **Badan Pusat Statistik (BPS)**.

Please refer to the original BPS publication and dataset documentation for information regarding data definitions, methodology, and usage rights.
