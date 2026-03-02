# Flight Delay Dataset - ETL Pipeline & Analysis

A comprehensive data pipeline project for extracting, transforming, loading, and visualizing airline delay data from the Kaggle Airline Delay dataset.

## Project Overview

This project implements a complete **Extract-Transform-Load (ETL)** pipeline combined with exploratory data analysis and visualization of airline delay patterns. The analysis covers flight delay causes, distribution patterns, and correlations between various delay factors across different carriers and airports.

**Dataset Source:** [Kaggle - Airline Delay Dataset](https://www.kaggle.com/datasets/sriharshaeedala/airline-delay/data)

---

## Table of Contents

- [Project Overview](#project-overview)
- [Project Structure](#project-structure)
- [Dataset Description](#dataset-description)
- [ETL Pipeline Phases](#etl-pipeline-phases)
  - [PHASE 1: Extract](#phase-1-extract)
  - [PHASE 2: Transform](#phase-2-transform)
  - [PHASE 3: Visualization](#phase-3-visualization)
  - [PHASE 4: Load](#phase-4-load)
- [Key Features](#key-features)
- [How to Use Locally](#how-to-use-locally)
- [Dependencies](#dependencies)
- [Results & Insights](#results--insights)

---

## Project Structure

```
flight-delay-dataset/
│
├── README.md                    # Project documentation
├── notebooks/
│   └── etl.ipynb               # Main ETL pipeline notebook
│
├── data/
│   ├── raw/
│   │   └── Airline_Delay_Cause.csv (original dataset)
│   └── processed/
│       └── cleaned_airline_data.csv (cleaned dataset)
│
└── requirements.txt            # Python dependencies
```

---

## Dataset Description

The dataset contains airline delay information structured at the granularity of **year, month, carrier, and airport combinations**.

### Key Columns:

**Temporal & Categorical:**
- `year` - Year of the data
- `month` - Month of the data
- `carrier` - Carrier code
- `carrier_name` - Full carrier name
- `airport` - Airport code
- `airport_name` - Full airport name

**Flight Counts:**
- `arr_flights` - Total number of arriving flights
- `arr_del15` - Number of flights delayed by 15+ minutes
- `arr_cancelled` - Number of cancelled flights
- `arr_diverted` - Number of diverted flights

**Delay Cause Counts:**
- `carrier_ct` - Delays due to carrier
- `weather_ct` - Delays due to weather
- `nas_ct` - Delays due to National Airspace System (NAS)
- `security_ct` - Delays due to security
- `late_aircraft_ct` - Delays due to late aircraft arrival

**Total Delay Times (in minutes):**
- `arr_delay` - Total arrival delay
- `carrier_delay` - Carrier-attributed delay
- `weather_delay` - Weather-attributed delay
- `nas_delay` - NAS-attributed delay
- `security_delay` - Security-attributed delay
- `late_aircraft_delay` - Late aircraft-attributed delay

---

## ETL Pipeline Phases

### PHASE 1: Extract

**Objective:** Load the raw airline delay dataset from Kaggle

**How it was done:**
- Used `kagglehub` library to directly fetch the dataset
- Loaded the CSV file into a Pandas DataFrame
- Verified data structure and initial shape
- Confirmed all 21 columns were properly loaded

**Code Highlights:**
```python
import kagglehub
from kagglehub import KaggleDatasetAdapter

file_path = "Airline_Delay_Cause.csv"
df = kagglehub.dataset_load(
    KaggleDatasetAdapter.PANDAS,
    "sriharshaeedala/airline-delay",
    file_path
)
```

**Output:** Raw DataFrame with 171,666 rows × 21 columns

---

### PHASE 2: Transform

**Objective:** Clean, process, and prepare data for analysis

**Transformations Applied:**

1. **Data Quality Checks**
   - Identified missing values and data types
   - Handled NaN values appropriately
   - Validated numeric ranges

2. **Data Cleaning**
   - Removed or imputed missing values
   - Corrected data type inconsistencies
   - Standardized categorical values

3. **Feature Engineering**
   - Created calculated columns for insights
   - Derived delay ratios (delayed flights / total flights)
   - Generated delay cause percentages

4. **Data Validation**
   - Ensured data consistency across rows
   - Verified temporal data integrity
   - Validated relationship between related columns

**Key Statistics Post-Transformation:**
- Clean dataset with no critical missing values
- All numeric columns properly typed
- Ready for visualization and analysis

---

### PHASE 3: Visualization

**Objective:** Generate insights through multiple visualization types

**Visualizations Created:**

1. **Correlation Analysis**
   - Heatmap showing correlation between all numeric columns
   - Identifies relationships between delay causes
   - Highlights strongly correlated variables

2. **Distribution Analysis**
   - Histograms/KDE plots for key delay metrics
   - Distribution of arrival delays
   - Distribution across months and carriers
   - Distribution of delay causes

3. **Additional Visualizations** (3+ more graphs):
   - **Box plots** - Delay distribution by carrier
   - **Bar charts** - Top airports by delay frequency
   - **Scatter plots** - Relationship between flight volume and delays
   - **Time series** - Seasonal patterns in delays
   - **Violin plots** - Distribution comparison across categories

**Libraries Used:**
- `seaborn` - Statistical data visualization
- `matplotlib` - Plotting library
- `pandas` - Data manipulation and visualization

---

### PHASE 4: Load

**Objective:** Save the cleaned and processed data for future use

**How it was done:**
- Exported cleaned DataFrame to CSV format
- Saved to `data/processed/cleaned_airline_data.csv`
- Maintained data integrity during export
- Documented column specifications

**Code:**
```python
df.to_csv('data/processed/cleaned_airline_data.csv', index=False)
```

---

## Key Features

✅ **Complete ETL Pipeline** - Extract, Transform, Visualize, and Load  
✅ **Data Quality Assurance** - Validation and cleaning procedures  
✅ **Comprehensive Visualizations** - 5+ different chart types  
✅ **Statistical Analysis** - Correlation and distribution analysis  
✅ **Actionable Insights** - Business intelligence from data  
✅ **Reproducible Code** - Well-documented Jupyter notebook  
✅ **Processed Dataset** - Clean CSV ready for further analysis  

---

## How to Use Locally

### Prerequisites
- Python 3.8 or higher
- Jupyter Notebook or JupyterLab
- Git

### Setup Instructions

**1. Clone the repository:**
```bash
git clone https://github.com/shaswat-13/flight-delay-dataset.git
cd flight-delay-dataset
```

**2. Create a virtual environment (recommended):**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

**3. Install dependencies:**
```bash
pip install -r requirements.txt
```

**4. Configure Kaggle API (for data download):**
```bash
# Follow instructions at: https://www.kaggle.com/settings/account
# Place kaggle.json in ~/.kaggle/ directory
chmod 600 ~/.kaggle/kaggle.json  # On Unix/Mac
```

**5. Open and run the notebook:**
```bash
jupyter notebook notebooks/etl.ipynb
```

**6. Execute cells sequentially:**
- Start from the top
- Each section is clearly marked (EXTRACT, TRANSFORM, LOAD)
- Run cells in order to maintain data pipeline flow

### Alternative: Run without Kaggle API
If you have the raw CSV file, place it in `data/raw/` and modify the extraction cell to:
```python
df = pd.read_csv('data/raw/Airline_Delay_Cause.csv')
```

---

## Dependencies

```
pandas>=1.3.0
numpy>=1.21.0
matplotlib>=3.4.0
seaborn>=0.11.0
jupyter>=1.0.0
kagglehub>=0.3.13
```

Install all dependencies with:
```bash
pip install -r requirements.txt
```

---

## Results & Insights

### Major Findings:

1. **Primary Delay Causes**
   - Late aircraft arrival is the leading cause of delays
   - Weather conditions significantly impact specific routes
   - Carrier-related delays vary considerably by airline

2. **Seasonal Patterns**
   - Summer months show higher delay frequencies
   - December peaks due to holiday travel and weather
   - Spring shows relatively stable delay patterns

3. **Airport Variations**
   - Larger hub airports experience different delay patterns
   - Regional airports show unique delay characteristics
   - Geographic factors influence delay distribution

4. **Carrier Performance**
   - Significant variation in delay performance across carriers
   - Some carriers consistently outperform in specific metrics
   - Operational efficiency varies by route

5. **Correlation Insights**
   - Strong correlation between flight volume and absolute delays
   - Weak correlation between different delay cause categories
   - Total delay time strongly correlated with all component delays

---

## Project Workflow Summary

```
┌─────────────────────────────────────────────────────────────┐
│                      START: Raw Data                        │
│          (Kaggle Airline Delay Dataset - 171K+ rows)        │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ PHASE 1: EXTRACT                                            │
│ ├─ Load data from Kaggle using kagglehub                   │
│ ├─ Verify data structure and shape                         │
│ └─ Display sample records                                   │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ PHASE 2: TRANSFORM                                          │
│ ├─ Handle missing values                                    │
│ ├─ Data type conversions                                    │
│ ├─ Feature engineering                                      │
│ ├─ Data validation and quality checks                       │
│ └─ Remove duplicates and inconsistencies                    │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ PHASE 3: VISUALIZATION & ANALYSIS                           │
│ ├─ Correlation heatmaps                                     │
│ ├─ Distribution plots (histograms, KDE)                    │
│ ├─ Categorical analysis (box plots, violin plots)           │
│ ├─ Time series and trend analysis                           │
│ └─ Generate insights and interpretations                    │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ PHASE 4: LOAD                                               │
│ ├─ Export cleaned data to CSV                              │
│ ├─ Maintain data integrity                                  │
│ └─ Ready for downstream analysis                            │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│        END: Processed Data + Insights Generated            │
│       (cleaned_airline_data.csv + Analysis Reports)        │
└─────────────────────────────────────────────────────────────┘
```

---

## Contact & Support

For questions or suggestions about this project:
- 📧 GitHub Issues: [Open an issue](https://github.com/shaswat-13/flight-delay-dataset/issues)
- 👤 GitHub Profile: [@shaswat-13](https://github.com/shaswat-13)

---

## License

This project is open source and available under the MIT License. Please ensure you comply with Kaggle's terms of service when using the dataset.

---

**Last Updated:** March 2026  
**Status:** ✅ Complete