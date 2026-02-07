## **Exploratory Data Analysis and Feature Engineering of S.S. Lootah Real Estate Portfolios**

### **Project Overview**

This project involved a comprehensive exploratory data analysis (EDA) and data cleaning of two core datasets from S.S. Lootah Real Estate: **Total Contracts** and **Unit Master**. The primary objective was to resolve data inconsistencies and engineer high-value features to produce decision-ready views on revenue trends, occupancy rates, and contract health. By applying robust cleaning techniques and visual analytics, the project successfully mapped monthly revenue performance for 2024 and 2025 and identified key occupancy benchmarks across the building portfolio.

### **Business Understanding**

The primary stakeholders for this project are the **executive leadership and asset managers at S.S. Lootah Real Estate**. In the high-volume Dubai real estate market, manual tracking of vast transactional and unit-level data often leads to "data silos" and reporting inaccuracies. The business problem centered on the need for a unified, clean data source to drive strategic decisions regarding revenue forecasting, lease renewals, and vacancy reduction. By automating the cleaning and KPI generation process, the organization can shift from reactive troubleshooting to proactive portfolio management, ensuring optimized cash flow and higher occupancy stability.

### **Data Understanding**

The analysis utilized two primary datasets:

* **Total Contracts:** Contained transactional data including contract amounts, types, and start/end dates.
* **Unit Master:** Contained unit-level details such as rental status, building names, and unit prices.
* **Timeframe:** The analysis specifically focused on revenue and transaction trends across the **2024 and 2025** fiscal periods.
* **Data Limitations:** Initial datasets contained varied date formats (using dots, dashes, and slashes), duplicate rows, and non-numeric symbols in currency fields. These inconsistencies required extensive normalization to ensure the accuracy of the downstream financial KPIs.

### **Modeling and Evaluation**

While this project was centered on **Exploratory Data Analysis (EDA)** rather than predictive modeling, it utilized a "Data Pipeline" model to evaluate and transform the raw information:

* **Cleaning Model:** Used **Type Casting** and **Date Normalization** (standardizing strings to `datetime` objects) and **De-duplication** to ensure a unique-row primary key structure.
* **Feature Engineering:** Developed custom features including `transaction_year`, `contract_length_year`, and `is_expired` flags to quantify contract health.
* **Evaluation Metrics:** The "success" of the data transformation was evaluated through:
* **Occupancy Rate %:** Mean of the engineered `occupancy_flag` across buildings.
* **Revenue Seasonality:** Distribution of transactions by month (Jan–Dec) to identify peak leasing periods.
* **Contract Duration Distribution:** Histogram analysis to identify standard 1-year tenures vs. outliers.

### **Conclusion**

The analysis reveals that the portfolio maintains a measurable seasonality in transactions, and the identification of expired contracts by building provides an immediate "hit list" for the leasing team to target for renewals. To solve the identified business problems, I recommend integrating these cleaned CSV outputs into a real-time **Tableau Executive Dashboard** to monitor the "Top 20 Buildings by Occupancy" and "Monthly Revenue Trends" dynamically.

**Future Steps:**

* **Predictive Churn Modeling:** Use the engineered `is_expired` and `contract_length` features to build a machine learning model that predicts the likelihood of a tenant vacating 90 days before expiry.
* **Price Optimization:** Correlate unit prices from the Unit Master with actual contract amounts to identify buildings that are currently under-priced relative to market demand.
