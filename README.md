# RFM-Customer-Segmentation-Analysis
This project is an end-to-end Business Analysis and Data Analysis project that transforms a large, raw, and "dirty" e-commerce dataset into an actionable strategic plan.
The analysis uses the **RFM (Recency, Frequency, Monetary)** framework to segment over 4,300 unique customers. The final output is a Power BI dashboard that clearly identifies high-value, at-risk, and low-value segments, leading to data-driven recommendations that can optimize marketing spend and improve customer retention.

# 📊 Final Power BI Dashboard


[RFM customer.pdf](https://github.com/user-attachments/files/23264209/RFM.customer.pdf)


## 1. Business Problem & Objective

* **Problem:** The company has low customer retention (a "leaky bucket") and inefficient marketing spend. It treats all customers the same, wasting resources on "Lost Customers" (30% of the database, 5% of revenue) and not protecting high-value "Champions" (11% of the database, 46% of revenue).
* **Objective:** To segment the entire customer base using RFM, identify the most valuable and at-risk groups, and propose a targeted marketing strategy to increase profitability and retention.

## 2. Methodology & Tools

This project was completed using a combination of BA frameworks and data analysis tools:

* **Framework:** RFM (Recency, Frequency, Monetary)
* **Tools:**
    * **Excel (Power Query):** For all major data cleaning and transformation (ETL).
    * **Excel (PivotTable & Formulas):** For data aggregation, RFM calculation, and scoring.
    * **Power BI:** For data visualization, dashboard creation, and insight generation.

## 3. The Process (Step-by-Step)

### Step 1: Data Cleaning (Excel Power Query)
The raw dataset contained 541,909 rows. It was cleaned to create a reliable dataset for analysis:
* **Removed Missing `CustomerID`s:** 135,080 rows were removed.
* **Removed Cancelled Orders:** 8,905 rows (where `InvoiceNo` started with 'C') were removed.
* **Removed Invalid Transactions:** 40 rows with a `UnitPrice` of 0 were removed.
* **Feature Engineering:** A `TotalPurchaseValue` column (`Quantity * UnitPrice`) was created.
* **Result:** A clean, analysis-ready dataset of **397,884 valid transactions**.

### Step 2: RFM Calculation (Excel PivotTable & Formulas)
The clean transaction data was aggregated into a customer-level table:
1.  **PivotTable:** A PivotTable (using the "Add to Data Model" option) was built to get:
    * **Monetary:** `Sum of TotalPurchaseValue`
    * **Frequency:** `Distinct Count of InvoiceNo`
    * **Recency:** `Max of InvoiceDate`
2.  **Formulas:**
    * `Recency (Days)` was calculated by subtracting the `Max of InvoiceDate` from a snapshot date (`2011-12-10`).
    * `PERCENTILE.INC` was used to find the four cut-off points (quintiles) for R, F, and M.
    * Nested `IF` formulas were used to assign **`R_Score`**, **`F_Score`**, and **`M_Score`** (from 1 to 5) to all 4,316 customers.

### Step 3: Segmentation (Excel Formulas)
Customers were assigned a segment name (e.g., "Champion", "At Risk") using an `IF(AND(...))` formula based on their R and F scores.

### Step 4: Visualization (Power BI)
The final, scored table was loaded into Power BI to create the dashboard, which includes:
* **KPI Cards:** Total Revenue ($16.03M) & Total Customers (4,316).
* **Donut Chart:** "Count of CustomerID by Segment" (Shows the *size* of each group).
* **Treemap:** "Sum of Monetary by Segment" (Shows the *value* of each group).
* **RFM Grid (Matrix):** A heatmap of "Count of CustomerID by R_Score and F_Score" (Shows the *health* and *density* of the customer base).

## 4. Key Insights & Recommendations

The dashboard tells a clear story:

* **Insight 1:** The business is heavily driven by the Pareto Principle. The **"Champions" (11% of customers) generate 46% ($7.37M) of all revenue.**
* **Insight 2:** A valuable group of **478 "At Risk" customers are worth $2.24M** and require immediate intervention.
* **Insight 3:** Marketing spend is inefficient. The **"Lost Customers" (30% of the base) contribute only 5% of revenue.**

Based on this, I recommend a 4-point strategic plan:
1.  **Protect "Champions":** Implement a VIP program with non-monetary perks (e.g., free shipping, early access) to reward loyalty.
2.  **Win-Back "At Risk":** Launch an aggressive, high-value discount campaign (e.g., 20% off) to reactivate this $2.24M segment.
3.  **Nurture "New Customers":** Create an onboarding campaign focused on driving a *second* purchase.
4.  **De-prioritize "Lost Customers":** Remove this segment from expensive marketing campaigns to cut waste and re-allocate the budget.
