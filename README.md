# Exoplanet Discovery Analytics  
### Data Visualization & Analytics (DVA) Capstone Project

---

## Project Information

- **Course:** Data Visualization and Analytics (DVA)  
- **Group Number:** 09  
- **Section:** C  
- **Project Title:** Understanding Exoplanet Discovery Patterns Using Data Analytics  

---

## Team Members

| S.No | Name             | Enrollment Number |
|-----:|------------------|-------------------|
| 1    | Krishna          | 2401010237 |
| 2    | Neeraj Singh     | 2401010297 |
| 3    | Satyam Singh     | 2401010430 |
| 4    | Rudraksh Rathod  | 2401010396 |
| 5    | Antik Mondal     | 2401010084 |
| 6    | Bineet Keshari   | 2401010130 |

---

## Project Overview

The discovery of exoplanets (planets outside our solar system) has accelerated due to advances in detection technologies. However, historical exoplanet datasets are strongly influenced by **observational bias, detection feasibility, and technological limitations**.

This project analyzes historical exoplanet data to:
- Evaluate discovery efficiency across methods
- Understand technology-driven discovery trends
- Identify bias in detected planet populations
- Support data-driven decision-making for future space missions

---

## Repository Structure (Mandatory)

```
├── RawDataset/
│ └── exoplanets_raw.csv
│
├── Cleaned/
│ ├── exoplanets_cleaned.csv
│ └── Cleaning_Log.md
│
├── Calculations_Pivots/
│ ├── pivot_tables.xlsx
│ └── derived_columns.csv
│
├── Dashboard/
│ └── Exoplanet_Dashboard.png
│
├── Documentation/
│ └── Project_Report.pdf
│
├── Presentation/
│ └── Final_Presentation.pptx
│
└── README.md
```

---

## Data Dictionary (Key Columns)

| Column Name | Description |
|------------|-------------|
| Planet Name | Unique identifier of the exoplanet |
| Mass (MJ) | Planet mass in Jupiter masses |
| Radius (RJ) | Planet radius in Jupiter radii |
| Orbital Period (days) | Time taken to complete one orbit |
| Distance (ly) | Distance from Earth in light years |
| Discovery Method | Technique used for detection |
| Discovery Year | Year of confirmation |
| Host Star Mass | Mass of the host star |
| Temperature (K) | Estimated planetary temperature |

Derived analytical columns:
- Mass Category (Small / Medium / Giant)
- Period Category (Ultra-Short / Short / Long)
- Distance Category (Near / Mid / Far)
- Host Star Type (Cool / Sun-like / Hot)

---

## Data Cleaning Notes

The raw dataset contained:
- Scientific uncertainty values (±, ranges, citations)
- Mixed numeric and text formats
- Inconsistent categorical naming
- High missing-value density

### Cleaning Actions
- Extracted best-estimate numeric values
- Removed uncertainty ranges and symbols
- Standardized measurement units
- Created analytical categories
- Ensured planet-level uniqueness

All cleaning steps were documented in `Cleaning_Log.md`.

---

## Key Insights & Statistics

- **Transit method** accounts for the majority of exoplanet discoveries
- Discovery volume increased sharply after **2005**, driven by technology
- **Large and close-in planets** are over-represented
- Imaging methods detect **fewer but massive and distant planets**
- Detection diversity decreases significantly with distance

---

## Dashboard Summary

The dashboard provides:

### Executive View
- Total exoplanets discovered
- Average distance from Earth
- Average host star temperature

### Operational View
- Discovery method dominance
- Bias across mass, distance, and orbital period
- Year-wise discovery trends
- Interactive filters for drill-down analysis

---

## Dataset Analysis Screenshots

Screenshots included in the `Dashboard/` folder:
- Discovery Method Dominance
- Discovery Trend Over Time
- Mass vs Discovery Method
- Distance vs Detection Method

These visuals support all insights discussed in the project.

---

## Recommendations

- Prioritize scalable transit survey missions
- Use radial velocity for confirmation
- Reserve imaging for distant massive planets
- Invest in high-sensitivity instruments
- Adopt hybrid detection strategies

---

## Limitations & Future Scope

### Limitations
- Observational and technological bias
- Incomplete physical parameters
- Limited post-2009 data

### Future Scope
- Integration of Kepler, TESS, JWST datasets
- Bias-correction modeling
- Advanced habitability analysis
- Real-time dashboard updates

---

## Technologies Used

- Google Sheets (Cleaning, Pivots, Dashboard)
- Spreadsheet Functions & Pivot Tables
- Looker Studio (optional)
- Markdown & PDF
- PowerPoint

---

## Conclusion

This project demonstrates that exoplanet discovery patterns are shaped more by **technology and feasibility** than by true planetary abundance. By acknowledging bias and constraints, the analysis provides realistic and decision-oriented insights for future space exploration strategies.

---
