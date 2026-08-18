# Master's Thesis Replication Package

This repository contains the raw data, code, intermediate data outputs, and econometric test results accompanying the master's thesis titled:
> **Price Discovery in FOMC Rate Expectations: Traditional vs. Preidction Markets**

## 1. Overview
This repository is structured to provide full transparency and reproducibility for the empirical findings presented in the thesis. The analysis investigates price discovery regarding FOMC rate expectations between traditional markets (CME FedWatch ZQ Futures) and modern prediction markets (Polymarket and Kalshi). The methodology encompasses a comprehensive, multi-step pipeline: gathering raw data from web sources (TradingView and Barchart) for CME futures, utilizing official APIs to extract Polymarket and Kalshi datasets, processing and harmonizing the data into appropriate formats, executing econometric tests (such as Granger causality, Vector Error Correction Models [VECM], and Forecast Error Variance Decomposition [FEVD]), and finally compiling the results across all collected events to present summary statistics and draw final conclusions.

## 2. System Requirements & Dependencies
* **Programming Language:** Python (tested on Python 3.14.3)
* **Key Libraries:** `pandas`, `numpy`, `statsmodels`, `arch`, `matplotlib`, `requests`


## 3. Visual Overview & Data Access

**Data Access**

> Due to GitHub's file size limits, the complete dataset (~600MB of raw and processed market files) is hosted externally. You can download the full `data/` folder via the link below and place it into your local repository root.

>  **[Download Thesis Dataset (Google Drive)]("https://drive.google.com/drive/folders/1L-yfRTiqvDhYenHyTAF_WXM6ThNWzcu3?usp=sharing")**

**Visual Overview**

```text
thesis_replication_package/
│
├── code/                      <-- All Python scripts and Jupyter notebooks
│   ├── 01_data_extraction/    <-- Scripts for extracting raw market data via APIs
│   ├── 02_cme_calculations/   <-- Individual Jupyter notebooks calculating CME implied probabilities
│   ├── 03_volume_preprocessing.py <-- Merges market data and computes volume tertiles
│   ├── 04_granger_causality/  <-- Granger causality testing scripts
│   ├── 05_vector_error_correction_model/ <-- VECM estimation scripts
│   ├── 06_forecast_error_variance_decomposition/ <-- FEVD scripts
│   └── 07_significance_reports/ <-- Scripts compiling statistical outputs into summary tables (corresponding to section "5. Results" in the written master thesis)
│
├── data/
│   ├── raw/                   <-- Untouched raw data exports (CME, Polymarket, Kalshi)
│   └── processed/             
│       ├── cme_implied_probs/ <-- Calculated CME implied probabilities per meeting month
│       └── volume.csv         <-- Consolidated trading volume data structured by tertiles
│
├── results/                   <-- Econometric model outputs and test results
│   ├── 01_granger_causality/   <-- Saved Granger causality test outputs
│   ├── 02_vector_error_correction_model/  <-- Saved VECM test outputs
│   └── 03_forecast_error_variance_decomposition/  <-- Saved FEVD outputs
│
├── README.md                  <-- Project documentation
└── requirements.txt           <-- Python package dependencies
```
## 4. Data Workflow 

1. **Raw Data Extraction (`data/raw/`)**
   * CME: Contains raw CME ZQ futures data downloaded from BarChart and TradingView, alongside data extracted from Peter Pavicic (https://github.com/PeterPavicic/MasterThesis).
   * Polymarket: Contains raw API extractions from Polymarket.
        * Event Extraction: Data must be extracted event-by-event by specifying the "slug" corresponding to the event of interest.
        * Slug Retrieval: Market slugs were retrieved directly from target platform URL endpoints.
        * Example: When viewing the event "Fed decision in April" (`https://polymarket.com/event/fed-decision-in-april`), the corresponding slug is `fed-decision-in-april`.

   * Kalshi: Contains raw API extractions from Kalshi (market slugs ere retrieved directly from target platform URL endpoints).
        * Event Extraction: Data must be extracted event-by-event by specifying the target ticker corresponding to the event of interest.
        * Target Ticker: Retrieved directly from target platform market event's URL endpoints.
        * Example: When viewing the event "Fed decision in April 2026?" (`https://kalshi.com/markets/kxfeddecision/fed-meeting/kxfeddecision-26apr?op_market_ticker=KXFEDDECISION-26APR-C25`), the corresponding ticker is "KXFEDDECISION-26APR-C25"

2. **CME Probability Calculations (`code/02_cme_calculations/`)**
   * Notebooks present compute the FedWatch implied probabilities for each specific FOMC meeting month. The first two initials of the notebook name (BP, FP, DBP) are indicative of the method used to calculate implied probabilities (see Section 4.1 for detailed information).
   * Outputs are exported directly to `data/processed/cme_implied_probs/`.

3. **Volume Processing (`code/03_volume_preprocessing.py`)**
  * Aggregates raw order-level trading volumes across CME, Polymarket, and Kalshi for all analyzed FOMC meetings into a unified timeline, saving the aggregated volume at the event level as the data grid data/processed/volume.csv.

4. **Econometric Testing (`code/04` through `code/06`)**
   * Executes time-series modeling including Granger causality, Vector Error Correction Models (VECM), and Forecast Error Variance Decomposition (FEVD), storing raw numerical outputs in the `results/` folder.

5. **Table Generation (`code/07_significance_reports/`)**
   * Aggregates empirical test results from the results/ directory to compile the final summary tables displayed in Section 5 (Results) of the master's thesis document.


## 5. Author Information
* **Author Name:** Raaif Mookanay
* **Degree Program:** Master of Science in Quantitative Finance
* **Institution:** Vienna University of Economics and Business 
* **Contact Email:** raaifriz@gmail.com

