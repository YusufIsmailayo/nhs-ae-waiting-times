# NHS A&E Waiting Times Pipeline

A end-to-end data engineering pipeline analysing NHS A&E 4-hour performance 
across England. Built using a Bronze→Silver→Gold medallion architecture.

**Key finding: The NHS 95% four-hour target has not been met in a single month 
across the 36 months from April 2022 to March 2025.**

## Project Overview

The NHS has a target that 95% of A&E patients should be seen within 4 hours 
of arrival. This pipeline ingests, transforms and analyses 36 months of 
provider-level performance data published by NHS England to measure how far 
the NHS is from that target — nationally, regionally, and by individual trust.

## Data Source

[NHS England — A&E Attendances and Emergency Admissions](https://www.england.nhs.uk/statistics/statistical-work-areas/ae-waiting-times-and-activity/)

- Monthly CSV files, April 2022 to March 2025
- ~200 NHS providers per month
- Provider level: NHS Trusts, UTCs, GP practices, independent sector

## Pipeline Architecture
Bronze → Silver → Gold
| Layer | Description | Output |
|---|---|---|
| Bronze | Raw CSV ingestion, saved as Parquet with audit columns | 36 Parquet files, 1,292 KB |
| Silver | Cleaned, typed, provider-classified, TOTAL rows separated | 7,238 rows, 250 KB |
| Gold | Metrics calculated, three analytical tables produced | Provider / National / Regional |

## Key Findings

- **0 out of 36 months** met the 95% four-hour target
- National Type 1 performance ranged from **54.3% (Dec 2023)** to **65.5% (Apr 2023)**
- **January 2025**: 61,529 patients waited 12+ hours after decision to admit — 
  the highest in the dataset
- Regional performance gap in March 2025: East of England 60.7% vs Midlands 58.6%
- Over **5,400 trust-months** of provider level data analysed

## Tech Stack

- Python (pandas, numpy)
- Parquet (pyarrow)
- JupyterLab / Anaconda
- Medallion architecture (Bronze→Silver→Gold)

## Notebooks

| Notebook | Purpose |
|---|---|
| `00_data_exploration.ipynb` | Initial data structure investigation |
| `01_bronze_ingestion.ipynb` | Downloads 36 monthly CSVs, saves as Parquet |
| `02_silver_transformation.ipynb` | Cleaning, typing, classification |
| `03_gold_layer.ipynb` | Metric calculation, analytical tables |

## Repository Structure
nhs-ae-waiting-times/
├── notebooks/
│   ├── 00_data_exploration.ipynb
│   ├── 01_bronze_ingestion.ipynb
│   ├── 02_silver_transformation.ipynb
│   └── 03_gold_layer.ipynb
├── data/                    # gitignored — regenerate by running notebooks
│   ├── bronze/
│   ├── silver/
│   └── gold/
├── .gitignore
└── README.md
## How to Reproduce

```bash
git clone https://github.com/YusufIsmailayo/nhs-ae-waiting-times.git
cd nhs-ae-waiting-times
pip install pandas pyarrow
jupyter lab
```

Then run notebooks 01 → 02 → 03 in order.

## Author

Yusuf Ismail — Data Engineer | NHS & Public Sector Analytics  
[GitHub](https://github.com/YusufIsmailayo) | 
[Medium](https://medium.com/@yusufismail_91982)