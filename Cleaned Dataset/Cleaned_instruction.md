# Data Cleaning and Feature Engineering Documentation: Exoplanets Dataset

---

## 1. Introduction

Data cleaning and preprocessing are among the most important steps in the data analysis lifecycle. Raw datasets often contain missing values, inconsistent formatting, incorrect entries, and structural issues that can affect the accuracy of analysis and machine learning models.

This project focuses on cleaning, preprocessing, and enriching the Exoplanets dataset. The objective was to transform the raw dataset into a structured, consistent, and analysis-ready format by resolving data quality issues and engineering new categorical features for better visualization.

---

## 2. Objective of the Project

The main objectives of this project were:
- To identify inconsistencies and noise in the raw dataset.
- To handle missing values appropriately using statistical imputation.
- To standardize categorical text formats and remove redundant spaces.
- To safely extract best-estimate numeric values from complex scientific notations.
- To engineer new categorical features from continuous numerical data to enhance exploratory data analysis.
- To identify and remove duplicate records.
- To prepare a clean dataset suitable for analysis and modeling.

---

## 3. Dataset Description

### 🔹 Raw Dataset
- **File Name:** `exoplanets.csv`
- **Format:** CSV
- **Type:** Uncleaned Dataset
- **Description:** Contains information related to discovered exoplanets and their various properties, featuring complex string-based scientific measurements.

### 🔹 Cleaned Dataset
- **File Name:** `Cleaned exoplanets.xlsx`
- **Format:** Google Sheet / Excel
- **Type:** Cleaned, Structured, and Enriched Dataset
- **Status:** Ready for Exploratory Data Analysis (EDA) and Visualization.

---

## 4. Issues Identified in the Raw Dataset

After examining the raw dataset, the following structural and formatting issues were found:
- **Presence of Missing Values:** Missing data points in both numerical and categorical columns.
- **Scientific Measurement Notations:** Numerical columns (Mass, Radius, Period, Temp) contained uncertainty values and special formats (e.g., `179.3±4.9` and `4319+151−130`).
- **Bracketed Citations:** Numerical and text columns contained reference-style brackets (e.g., `1.25 [2]`, `[37]`).
- **Inconsistent Categorical Text:** The Discovery Method column contained inconsistent casing and synonyms (e.g., "radial vel." vs. "Radial Velocity").
- **Duplicate Records:** The dataset contained duplicate rows for certain planets, which could lead to biased analysis and incorrect statistical results.

---

## 5. Data Cleaning Process

The data cleaning process was carried out in a structured, step-by-step manner:

### 🔹 Handling Missing Values
Missing values were identified using filtering and inspection techniques.
- **Numerical Columns:** Missing values were replaced using the **Median** function to reduce the impact of outliers.
- **Categorical Columns:** Missing values were filled using the **Mode** (most frequently occurring value).
- **Reason for Choosing Median:** Median is less sensitive to extreme values compared to the mean, making it a robust choice for skewed data.

### 🔹 Handling Scientific Notation and Uncertainty Values
The dataset included complex scientific values such as `179.3±4.9`, `4319+151−130`, and `1.25 [2]`. These formats cannot be directly used in numerical calculations because visualization tools interpret them as text.

**Action Taken:** Extracted the primary numeric "best estimate" value before any special symbols, ranges, or citations.
- `179.3±4.9` → `179.3`
- `4319+151−130` → `4319`
- `1.25 [2]` → `1.25`

**Formula Used:** Applied advanced Regular Expressions (Regex) to substitute commas and extract the leading number:
```excel
=IFERROR(VALUE(REGEXEXTRACT(SUBSTITUTE(TO_TEXT(reference_column), ",", ""), "^-?[0-9]*\.?[0-9]+")), reference_column)
```
### 🔹 Formatting and Categorical Standardization
To ensure visualizations group correctly, text columns required standardization.

**Action Taken:**
- Standardized column names and removed extra spaces.
- Used the `=PROPER(TRIM(cell))` formula to enforce Title Case and remove invisible leading/trailing spaces.
- Utilized Find & Replace to merge synonyms (e.g., changing "Radial Vel." to "Radial Velocity").

### 🔹 Removal of Duplicate Records
The dataset was examined for duplicate entries to ensure data integrity.

**Action Taken:**
- Used Google Sheets’ conditional formatting and sorting features to identify repeated rows.
- Removed duplicate records while preserving the first occurrence/most complete row.

**Reason:** Duplicate records can skew statistical calculations, bias model training, and misrepresent frequency-based analysis. After removal, the dataset contained only unique records.

---

## 6. Feature Engineering and Data Enrichment

To facilitate better exploratory data analysis (EDA) and allow for categorical visualizations (like pie charts and grouped bar charts), several new features were engineered from the continuous numerical data using nested conditional logic:

- **Mass Category:** Grouped planets into "Small", "Medium", or "Giant" based on mass.
  - *Formula:*
    ```excel
    =IF(B2<0.1, "Small", IF(B2<1, "Medium", "Giant"))
    ```

- **Radius Category:** Grouped planets into "Small", "Medium", or "Large" based on their radius.
  - *Formula:*
    ```excel
    =IF(C2<0.5, "Small", IF(C2<1.5, "Medium", "Large"))
    ```

- **Period Category:** Categorized the orbital periods into "Ultra Short", "Short", or "Long".
  - *Formula:*
    ```excel
    =IF(D2<10, "Ultra Short", IF(D2<100, "Short", "Long"))
    ```

- **Distance Category:** Grouped the distances from Earth into "Nearby", "Mid-Range", or "Far".
  - *Formula:*
    ```excel
    =IF(I2<100, "Nearby", IF(I2<500, "Mid-Range", "Far"))
    ```

- **Star Temp Category:** Categorized host star temperatures into "Cool", "Sun-like", or "Hot".
  - *Formula:*
    ```excel
    =IF(K2<4000, "Cool", IF(K2<6000, "Sun-like", "Hot"))
    ```

- **Is Habitable (Binary Flag):** Created a binary classification (1 = Yes, 0 = No) to identify potentially habitable exoplanets based on a combination of Planet Radius, Planet Temperature, and Host Star Temperature.
  - *Formula:*
    ```excel
    =IF(AND(C2>0, C2<=0.2, F2>=200, F2<=350, K2>=3000, K2<=7000), 1, 0)
    ```

---

## 7. Before and After Comparison

| Issue/Feature | Before Processing | After Processing |
| :--- | :--- | :--- |
| **Missing Values** | Present | Imputed (Median/Mode) |
| **Scientific Notations (±, + -)** | Present (Text format) | Extracted Base Value (Numeric) |
| **Bracketed Citations ([2])** | Present | Removed |
| **Categorical Text** | Mixed / Inconsistent | Standardized |
| **Duplicate Planets** | Present | Removed (Unique records only) |
| **Data Categorization** | Continuous Numbers Only | Categorical Groupings Engineered |

---

## 8. Tools and Techniques Used

The following tools and functions were used during the cleaning and engineering process:

- **Tool:** Google Sheets
- **Functions:** `MEDIAN()`, `MODE()`, `REGEXEXTRACT()`, `SUBSTITUTE()`, `IFERROR()`, `TRIM()`, `PROPER()`, `VALUE()`, `IF()`, `AND()`
- **Techniques:** Regular Expressions (Regex), Feature Engineering, Conditional Logic, Data Validation, Filtering and Sorting.

---

## 9. Challenges Faced

- Handling multiple types of inconsistencies simultaneously.
- Safely extracting base values from complex scientific string representations without losing data integrity.
- Choosing appropriate statistical methods for imputation.
- Defining accurate thresholds for the new categorical groupings (e.g., habitability parameters).

---

## 10. Final Outcome

The final cleaned dataset (`Cleaned exoplanets.xlsx`) is:
- Free from missing values and scientific text noise.
- Logically consistent and uniformly formatted.
- Enriched with categorical groupings and habitability flags.
- Structurally organized with unique records.
- Ready for Exploratory Data Analysis (EDA) and modeling.

---

## 11. Conclusion

The Exoplanets dataset was successfully cleaned, transformed, and enriched into a structured and reliable format. All major data quality issues were resolved through systematic preprocessing techniques, including statistical imputation and advanced text-parsing. Furthermore, feature engineering provided new dimensions for analysis. This project demonstrates the importance of data cleaning in real-world data science workflows and highlights practical skills in preparing complex scientific datasets for further analysis.