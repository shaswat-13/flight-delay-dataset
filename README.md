# Flight Delay Dataset - ETL Pipeline & Analysis

A comprehensive data pipeline project for extracting, transforming, loading, and visualizing airline delay data from the Kaggle Airline Delay dataset.

## Project Overview

This project implements a complete **Extract-Transform-Load (ETL)** pipeline combined with exploratory data analysis and visualization of airline delay patterns. The analysis covers flight delay causes, distribution patterns, and correlations between various delay factors across different carriers and airports.

**Dataset Source:** [Kaggle - Airline Delay Dataset](https://www.kaggle.com/datasets/sriharshaeedala/airline-delay/data)

---

## Project Structure

```
flight-delay-dataset/
│
├── README.md                    # Project documentation
├── notebooks/
│   └── etl.ipynb               # Main ETL pipeline notebook
├── data/
│   └── transform.csv (cleaned dataset)
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
   - Removed missing values
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
   - Histograms plots for key delay metrics
   - Distribution of arrival delays
   - Distribution across months and carriers
   - Distribution of delay causes

3. **Additional Visualizations** (3+ more graphs):
   - **Box plots** - Delay distribution by carrier
   - **Time series** - Seasonal patterns in delays


**Libraries Used:**
- `seaborn` - Statistical data visualization
- `matplotlib` - Plotting library
- `pandas` - Data manipulation and visualization

---

### PHASE 4: Load

**Objective:** Save the cleaned and processed data for future use

**How it was done:**
- Exported cleaned DataFrame to CSV format
- Saved to `data/transform.csv`
- Documented column specifications

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
│ ├─ Load data from Kaggle using kagglehub                    │
│ ├─ Verify data structure and shape                          │
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
│ ├─ Distribution plots (histograms)                          │
│ ├─ Categorical analysis (box plots)                         │
│ ├─ Time series and trend analysis                           │
│ └─ Generate insights and interpretations                    │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ PHASE 4: LOAD                                               │
│ ├─ Export cleaned data to CSV                               │
│ ├─ Maintain data integrity                                  │
│ └─ Ready for downstream analysis                            │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│        END: Processed Data + Insights Generated             │
│                  (transform.csv)                            │
└─────────────────────────────────────────────────────────────┘
```

---
**Last Updated:** March 2026  
