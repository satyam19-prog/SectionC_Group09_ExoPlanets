### Data Cleaning Log

| Column Name | Original State / Issues Identified | Cleaning Action / Transformation Applied | Final State / Output |
| :--- | :--- | :--- | :--- |
| **Planet Name** | Invisible trailing/leading spaces; Duplicate planet entries. | Applied `=TRIM()`; Highlighted and removed duplicate rows based on this primary key. | Clean String (Unique identifiers only) |
| **Mass (MJ)** | Scientific notation (e.g., `13.3±1.7`), missing values. | Extracted base value using `REGEXEXTRACT()`; Imputed missing values with Median. | Float (2 decimal places) |
| **Radius (RJ)** | Error margins (e.g., `5.8+1.4−1.0`), missing values. | Extracted base value using `REGEXEXTRACT()`; Imputed missing values with Median. | Float (2 decimal places) |
| **Period (days)** | Commas in large numbers (e.g., `25,000`), error bounds, missing values. | Removed commas with `SUBSTITUTE()`; Extracted base value; Imputed missing with Median. | Float (Numeric) |
| **Temp. (K)** | Commas, error margins, missing values. | Removed commas; Extracted base value; Imputed missing with Median. | Integer |
| **Distance (ly)** | Error margins, citations, missing values. | Extracted base value using `REGEXEXTRACT()`; Imputed missing with Median. | Float (Numeric) |
| **Discovery Method** | Inconsistent casing ("radial vel."), extra spaces, missing values. | Applied `=PROPER(TRIM())`; Used Find/Replace to merge synonyms; Imputed missing with Mode. | Categorical String |
| **Discovery Year** | Missing values, inconsistent data types. | Verified 4-digit year format; Imputed missing values with Mode (most frequent year). | Integer (YYYY format) |
| **Host Star Mass ($M_{\odot}$)** | Citations (`1.05 [2]`), error margins, missing values. | Extracted base value using Regex; Imputed missing with Median. | Float (2 decimal places) |
| **Host Star Temp. (K)** | Commas, citations, missing values. | Removed commas; Extracted base value using Regex; Imputed missing with Median. | Integer |
| **Remarks** | Bracketed citations (`[37]`), inconsistent blanks ("No remarks"). | Removed citations using Regex replace `\[\d+\]`; Standardized all empty variants to `"None"`. | Clean Text String |
| **Mass Category** | *New Feature Engineered from Mass (MJ)* | Applied nested `IF()`: `<0.1` (Small), `<1` (Medium), else (Giant). | Categorical (Small/Medium/Giant) |
| **Radius Category** | *New Feature Engineered from Radius (RJ)* | Applied nested `IF()`: `<0.5` (Small), `<1.5` (Medium), else (Large). | Categorical (Small/Medium/Large) |
| **Period Category** | *New Feature Engineered from Period* | Applied nested `IF()`: `<10` (Ultra Short), `<100` (Short), else (Long). | Categorical (Ultra Short/Short/Long) |
| **Distance Category**| *New Feature Engineered from Distance* | Applied nested `IF()`: `<100` (Nearby), `<500` (Mid-Range), else (Far). | Categorical (Nearby/Mid-Range/Far) |
| **Star Temp Category**| *New Feature Engineered from Host Star Temp* | Applied nested `IF()`: `<4000` (Cool), `<6000` (Sun-like), else (Hot). | Categorical (Cool/Sun-like/Hot) |
| **Is Habitable** | *New Feature Engineered from Multiple Columns* | Applied `IF(AND())` logic using optimal threshold ranges for Radius, Temp, and Star Temp. | Binary (1 = Yes, 0 = No) |