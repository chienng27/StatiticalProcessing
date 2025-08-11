# Body Performance Data Analysis Project

## 📊 Project Overview

This project focuses on analyzing body performance data to classify individuals into different performance categories (A, B, C, D) based on various physical and health metrics. The analysis employs exploratory data analysis (EDA), statistical modeling, and machine learning techniques to understand the factors influencing body performance.

**Date:** January 8, 2025

## 📁 Project Structure

```
Statistical processing/
├── bodyPerformance.csv          
├── Statistical processing.rmd  
├── Statistical processing.html  
├── Statistical processing.pdf  
├── SLIDE.pdf                   
└── README.md                   
```

## 📈 Dataset Description

The `bodyPerformance.csv` dataset contains 13,395 records with the following variables:

### Features:
- **age** - Age of the individual
- **gender** - Gender (M/F)
- **height_cm** - Height in centimeters
- **weight_kg** - Weight in kilograms
- **body fat_%** - Body fat percentage
- **diastolic** - Diastolic blood pressure
- **systolic** - Systolic blood pressure
- **gripForce** - Grip force measurement
- **sit and bend forward_cm** - Flexibility test result
- **sit-ups counts** - Number of sit-ups completed
- **broad jump_cm** - Broad jump distance in centimeters

### Target Variable:
- **class** - Performance classification (A, B, C, D)

## 🔬 Methodology

### 1. Exploratory Data Analysis (EDA)

#### 1.1 Data Structure Examination
- **Data Information Analysis**: Comprehensive function to examine data types, unique values, null values, and duplicates
- **Initial Data Overview**: Examination of 13,395 records with 12 variables
- **Data Type Conversion**: Converting categorical variables (gender, class) to factors
- **Missing Value Analysis**: Using VIM package to visualize missing data patterns

#### 1.2 Data Quality Assessment
- **Invalid Value Detection**: Identifying and removing records with zero values in critical variables:
  - Diastolic blood pressure = 0
  - Systolic blood pressure = 0
  - Grip force = 0
  - Sit and bend forward = 0
  - Sit-ups counts = 0
  - Broad jump = 0
- **Outlier Detection**: Using IQR method (1.5 × IQR) to identify and remove outliers from numeric variables
- **Data Cleaning Results**: Tracking data reduction from original to cleaned dataset

#### 1.3 Descriptive Statistics
- **Summary Statistics**: Comprehensive statistical summaries for all variables
- **Group-wise Analysis**: Performance metrics grouped by:
  - Gender (Male/Female)
  - Performance class (A/B/C/D)
  - Age groups (21-32, 33-44, 45-56, 56-64)
  - Body fat categories (<15%, 15-25%, >25%)
  - Height groups (<160cm, 160-170cm, >170cm)

#### 1.4 Data Visualization
- **Histogram Analysis**: Distribution plots for all numeric variables
- **Box Plots**: Comparative analysis across:
  - Age groups vs. performance metrics
  - Performance classes vs. physical indicators
  - Gender differences in physical measurements
- **Correlation Analysis**: Pearson correlation matrix with threshold analysis (>0.6 and <-0.6)
- **Density Ridge Plots**: Distribution visualization for each variable by performance class
- **Bar Charts**: Gender distribution across performance classes

### 2. Feature Engineering

#### 2.1 Derived Variables
- **BMI Calculation**: `BMI = weight_kg / (height_cm/100)²`
- **MAP Calculation**: `MAP = diastolic + (systolic - diastolic) / 3`
- **Age Grouping**: Categorical age groups (21-32, 33-44, 45-56, 56-64)
- **BMI Status Classification**:
  - Underweight: BMI < 18.5
  - Healthy: BMI 18.5-24.9
  - Overweight: BMI 25-29.9
  - Obese: BMI ≥ 30

#### 2.2 Data Transformation
- **Categorical Encoding**: Converting categorical variables to numeric codes
- **Feature Selection**: Removing redundant variables (weight, height, BMI) while keeping derived features
- **Data Type Standardization**: Ensuring consistent data types across variables

### 3. Statistical Testing (A/B Testing)

#### 3.1 Parametric Tests
- **ANOVA Testing**: For normally distributed variables (BMI, MAP, broad jump)
- **Assumption Verification**: Testing for normal distribution and homogeneity of variance

#### 3.2 Non-Parametric Tests
- **Dunn Test**: For non-normally distributed variables with Bonferroni correction:
  - Age vs. performance class
  - Body fat percentage vs. performance class
  - Grip force vs. performance class
  - Flexibility vs. performance class
  - Sit-ups counts vs. performance class

#### 3.3 Chi-Square Testing
- **Categorical Association**: Testing relationship between gender and performance class

### 4. Data Preprocessing for Modeling

#### 4.1 Class Balance Adjustment
- **Stratified Sampling**: Creating balanced dataset for binary classification
- **Data Splitting**: 80% training, 20% testing with stratification
- **Feature Selection**: Final model features:
  - Body fat percentage
  - Grip force
  - Sit and bend forward (flexibility)
  - Sit-ups counts
  - Broad jump distance
  - BMI status
  - MAP (Mean Arterial Pressure)

#### 4.2 Data Preparation
- **Missing Value Handling**: Complete case analysis
- **Feature Scaling**: Standardization of numeric variables
- **Categorical Encoding**: Proper encoding for machine learning algorithms

### 5. Statistical Modeling

#### 5.1 Random Forest Classification
- **Algorithm**: Random Forest with 500 trees
- **Features**: 7 engineered features
- **Parameters**:
  - `ntree = 500`
  - `importance = TRUE`
  - Stratified sampling for class balance
- **Model Evaluation**: Confusion matrix and accuracy metrics

#### 5.2 Multinomial Logistic Regression
- **Algorithm**: Multinomial logistic regression using `nnet::multinom`
- **Features**: Same feature set as Random Forest
- **Multiclass Classification**: Predicting A/B/C/D performance categories
- **Model Evaluation**: Confusion matrix and overall accuracy

### 6. Model Evaluation

#### 6.1 Performance Metrics
- **Confusion Matrix**: Detailed classification results
- **Accuracy**: Overall model performance
- **Class-wise Performance**: Performance for each performance category
- **Cross-validation**: Ensuring model robustness

#### 6.2 Model Comparison
- **Algorithm Comparison**: Random Forest vs. Multinomial Logistic Regression
- **Feature Importance**: Random Forest feature importance ranking
- **Model Selection**: Based on accuracy and interpretability

### 7. Advanced Analytics

#### 7.1 Age-based Analysis
- **Age Group Performance**: Comparative analysis across age groups
- **Body Fat Trends**: Body fat percentage patterns by age and performance
- **BMI Patterns**: BMI distribution across age groups and performance classes
- **MAP Analysis**: Mean arterial pressure trends by age and performance

#### 7.2 Gender-based Insights
- **Performance Differences**: Gender-specific performance patterns
- **Physical Metrics**: Gender differences in grip force, flexibility, and endurance
- **Health Indicators**: Gender-specific health metric distributions

## 🛠️ Technical Requirements

### R Packages Used:
```r
library(boot)
library(rsample)
library(tidyverse)
library(matrixStats)
library(lubridate)
library(janitor)
library(ggplot2)
library(corrplot)
library(dplyr)
library(splines2)
library(mgcv)
library(mgcViz)
library(leaps)
library(gridExtra)
library(grid)
library(MASS)
library(lmPerm)
library(DataExplorer)
library(caret)
library(splines)
library(ggridges)
library(ggbeeswarm)
library(readr)
library(randomForest)
library(VIM)
library(knitr)
library(car)
library(FSA)
```

## 📖 How to Use

### Prerequisites
- **R** (version 4.0 or higher)
- **RStudio** (recommended for interactive analysis)
- **Required R packages** (install using `install.packages()`)

### Installation and Setup
1. **Clone or download** the project files to your local machine
2. **Open RStudio** and set the working directory to the project folder
3. **Install required packages** if not already installed:
   ```r
   # Core packages
   install.packages(c("tidyverse", "caret", "randomForest", "corrplot", "ggplot2"))
   
   # Additional packages for full functionality
   install.packages(c("VIM", "FSA", "nnet", "rsample", "janitor"))
   ```

### Running the Analysis
1. **Open** `Statistical processing.rmd` in RStudio
2. **Check package dependencies** - ensure all required packages are loaded
3. **Knit the document** to generate HTML/PDF reports:
   - Click "Knit" button in RStudio, or
   - Run: `rmarkdown::render("Statistical processing.rmd")`
4. **Monitor progress** - the analysis may take several minutes to complete

### Viewing Results
- **Interactive Analysis**: Open `Statistical processing.html` in a web browser for interactive exploration
- **PDF Report**: Open `Statistical processing.pdf` for a formatted, printable report
- **Presentation**: View `SLIDE.pdf` for presentation slides
- **Raw Data**: Examine `bodyPerformance.csv` for the original dataset

### Troubleshooting
- **Package Issues**: If packages fail to install, try updating R and RStudio
- **Memory Issues**: For large datasets, ensure sufficient RAM (4GB+ recommended)
- **Encoding Issues**: Use `locale(encoding="latin1")` for proper character encoding

## 📊 Key Findings

### Performance Classification Insights
- **Class Distribution**: Analysis of performance categories A, B, C, D across different demographics
- **Feature Importance**: Ranking of physical and health metrics in predicting performance
- **Model Performance**: Comparison between Random Forest and Multinomial Logistic Regression accuracy
- **Demographic Patterns**: Age and gender-based performance variations

### Statistical Significance
- **ANOVA Results**: Significant differences in BMI, MAP, and broad jump across performance classes
- **Dunn Test Findings**: Non-parametric analysis revealing performance class differences
- **Chi-Square Results**: Gender-performance class associations

### Health and Fitness Correlations
- **Body Composition**: Relationship between body fat percentage and performance
- **Physical Fitness**: Grip force, flexibility, and endurance correlations
- **Cardiovascular Health**: Blood pressure patterns across performance levels
- **Age-related Trends**: Performance decline patterns with age

### Model Performance
- **Random Forest Accuracy**: Classification performance with feature importance ranking
- **Multinomial Logistic Regression**: Multiclass classification results
- **Cross-validation**: Model robustness assessment
- **Confusion Matrix Analysis**: Detailed classification accuracy by performance category

## 🔍 Data Quality

- **Dataset Size**: 13,395 records
- **Missing Values**: Analyzed and handled appropriately
- **Data Types**: Mixed (numeric and categorical)
- **Class Distribution**: Balanced through sampling techniques

## 📝 Notes

### Analysis Characteristics
- **Bilingual Documentation**: Analysis includes both Vietnamese and English comments for accessibility
- **Reproducible Results**: Set seed values ensure consistent results across runs
- **Comprehensive Metrics**: Model performance metrics are included in the final report
- **Advanced Feature Engineering**: BMI and MAP calculations for enhanced analysis

### Technical Considerations
- **Data Encoding**: Latin1 encoding used for proper character handling
- **Memory Management**: Efficient data processing for large dataset (13,395 records)
- **Statistical Rigor**: Proper statistical testing with corrections for multiple comparisons
- **Model Validation**: Cross-validation and stratified sampling for robust results

### Research Applications
- **Health Assessment**: Useful for fitness professionals and health researchers
- **Performance Prediction**: Can assist in predicting body performance categories
- **Demographic Analysis**: Insights into age and gender-based performance patterns
- **Educational Tool**: Comprehensive example of statistical analysis workflow

## 📄 License

This project is for educational and research purposes.

## 📚 Additional Resources

### Documentation Files
- **R Markdown**: `Statistical processing.rmd` - Complete analysis code and documentation
- **HTML Report**: `Statistical processing.html` - Interactive web-based report
- **PDF Report**: `Statistical processing.pdf` - Printable formatted report
- **Presentation**: `SLIDE.pdf` - Presentation slides for project overview

### Data Source
- **Dataset**: `bodyPerformance.csv` - Original dataset with 13,395 records
- **Variables**: 12 features including demographic, physical, and health metrics
- **Target**: Performance classification (A, B, C, D)

### Contact Information
For questions about this analysis or collaboration opportunities, please contact the team members listed in the project overview.

---

**Last Updated**: January 8, 2025  
**Project Status**: Complete  
**Analysis Type**: Statistical Classification and Prediction
#   S t a t i t i c a l P r o c e s s i n g 
 
 
