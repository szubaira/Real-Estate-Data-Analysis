# S.S. Lootah Real Estate — Exploratory Data Analysis (EDA)

This project explores and cleans two core datasets from S.S. Lootah Real Estate — **Total Contracts** and **Unit Master** — to produce reliable, decision-ready views on **revenue**, **occupancy**, and **contract health**.  
It includes robust data cleaning (type casting, date normalization, de-duplication), engineered features (transaction year/month, contract duration, occupancy flags), and visual analyses (monthly revenues, transactions, occupancy by building, expiries).

**Highlights**
- Cleaned and validated transactional and unit-level datasets
- KPIs & visuals: monthly revenue (2024/2025), transactions by month, contract duration distribution, occupancy %, top-20 buildings by occupancy, and expired contracts by building
- Exported clean CSVs for **Tableau** or downstream analytics

---

## Repository Structure

Paths in the script are set for Colab (`/content/...`). If running locally, either mimic this structure or update the paths.

---

## Data Inputs

**1) Total Contracts** (`Total Contracts-Table 1.csv`)  
- Key columns used in the script:
  - `Amount` (revenue), `Type`  
  - `Transaction Date` → parsed to `transaction_year`, `transaction_month_name`  
  - `Contract Start Date`, `Contract End Date` → parsed to datetimes  
  - `Property Name.` (used for building-level grouping)

**2) Unit Master** (`Unit Master-Table 1.csv`)  
- Key columns used:
  - `Rental Status` (mapped to occupancy flag)  
  - `Price` (cleaned to numeric)  
  - `Building Name` (group level for occupancy)

---

## Data Cleaning & Feature Engineering

**Contracts (df)**
- Strip and coerce `Amount` to numeric (remove symbols, cast to float)
- Normalize date strings (`-`, `.` → `/`) then parse to `datetime`
- Build calendar features:
  - `transaction_year`  
  - `transaction_month_name` (ordered Jan→Dec)
- Remove duplicate rows
- **Contract tenure**: `contract_length_year` from start/end dates
- **Expiry flag**: `is_expired = 1` if `Contract End Date` < *today*

**Units (df_1)**
- Clean `Price` to numeric
- De-duplicate rows
- **Occupancy flag**: map `Rental Status` to {LEASED/BOOKED → 1, VACANT/EXPIRED → 0}
- **Building-level occupancy**: mean of `occupancy_flag` × 100

---

## Key Analyses & Visuals

The script uses **pandas**, **numpy**, **matplotlib**, and **seaborn**.

1) Revenue Trends**
   - Total revenue by `transaction_year`
   - Average revenue for 2024 and 2025
   - Total revenue by `transaction_month_name` for 2024 and 2025
   - Distribution of `Type`

2) **Transactions Seasonality**
   - Histogram of transactions by month (Jan–Dec)

3) **Contract Health**
   - Histogram of `contract_length_year` (typical 1-year, with outliers)
   - `is_expired` flag + **expired contracts per building**

4) **Occupancy**
   - Overall occupancy rate (mean of `occupancy_flag`)
   - **Top 20 buildings by occupancy rate** (bar chart)

These visuals support executive dashboards (e.g., in Tableau) for **Revenue**, **Occupancy**, **Expired Contracts**, and **Seasonality**.

---

## How to Run

### Option A — Google Colab
1. Upload both raw CSVs to your Colab workspace.
2. Open `src/updated_realestate_eda_python.py` in Colab (or copy its content into a notebook cell).
3. Ensure file paths point to `/content/Total Contracts-Table 1.csv` and `/content/Unit Master-Table 1.csv`.
4. Run all cells. Clean CSVs will be saved as:
   - `/content/Cleaned_Totalcontracts_Data.csv`
   - `/content/Cleaned_units_data.csv`

### Option B — Local (venv)
```bash
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python src/updated_realestate_eda_python.py
