# Financial-Sales-Dashboard-with-Automation
A Power BI-centric solution that transforms a manual, error-prone financial data workflow into an automated, cost-efficient pipeline, delivering key customer segmentation and Lifetime Value (LTV) insights to the end User.

---
# 📊 US Financial Data Analysis Dashboard

This project contains a comprehensive Power BI report developed to address critical data processing and analytical challenges faced by a team analysing US financial data for the US government client.

The solution automates a manual, error-prone workflow and delivers deep insights into customer financial behaviour, demographics, and LTV (Lifetime Value) scoring to tailor credit strategies and promotions.

## 💡 Problem & Automated Solution

The initial process involved manually receiving, downloading, combining (approx. 25 files daily), and cleaning data before a dashboard could be built by 8 PM. This process was time-consuming, error-prone, and costly due to additional staff hired.

| Challenge | Power BI / Power Query Solution | Result |
| :--- | :--- | :--- |
| **Manual Data Workflow** | **Automated Data Pipeline (Power Query)**: Configured scheduled refresh and automated combining/cleaning of files. | **Time & Error Reduction**: Reduced reliance on manual steps and minimised data manipulation errors. |
| **Increased Labor Costs** | **Process Streamlining**: The solution required less manual oversight. | **Cost Reduction**: Eliminated the need for the two additional employees, saving **$\text{\$12,000}$ per month**. |

### **Automated Data Pipeline (ETL)**

The following hybrid solution was implemented to manage the daily influx of approximately 25 files, ensuring data was consolidated and ready for the Power BI model:

1.  **Email Standardisation & Filtering:** Mail senders were instructed to include **"Credit Score"** in the email subject line. This keyword was used as a rule to filter the daily files into a separate folder automatically.
2.  **Cloud Transfer (Power Automate):** **Power Automate** was configured to monitor this dedicated email folder and automatically transfer all attachment files to a specific directory within **Google Drive**.
3.  **Data Integration (Power BI & API):** An **API connection** was established to link Google Drive directly to the Power BI service, ensuring a live connection to the raw files.
4.  **Data Processing & Combination (Python):** A **Python script** utilising the **`google-auth`** library was used to access the files in Google Drive. This script performed the critical task of **reading and combining all individual files** into a single consolidated dataset, which the Power BI model then consumed to solve the analytical requirements.
5.  **Manual Cleanup:** The only non-automated step remaining in the pipeline is the **manual deletion** of the old daily data from Google Drive to manage storage and ensure a clean environment for the next day's upload.

---

## 🛠️ Technical Implementation: Analysis & DAX

The core of the report is built upon Power Query for robust ETL (Extract, Transform, Load) and DAX (Data Analysis Expressions) for complex metric creation.

### 1. Key Metrics and Distribution (Questions 1, 3)

| Requirement | DAX Measure / Visualisation |
| :--- | :--- |
| **Core Financial Metrics** | [cite_start]Simple DAX **`AVERAGE`** measures for: Average Annual Income, Average Monthly Balance, Average number of payment delays, and Average Credit Utilisation. |
| **Age Demographics** | [cite_start]**Histogram** visualisation showing the frequency and distribution of customer ages, aiding targeted marketing. |

### 2. Customer Segmentation and LTV (Questions 4, 7, 8)

This involved creating calculated columns and complex measures for value assessment:

#### A. Age Grouping (Question 4)

[cite_start]A **DAX Calculated Column** was created to define fixed age segments for cross-analysis:

* **14-19:** "Teen"
* **19-25:** "Young Adult"
* **25-35:** "Old Adult"
* **35-45:** "Old1"
* **$>$45:** "Old2"

This column was used in a visual to show the count of people within each group against different **Credit Scores**.

#### B. Potential Customer Identification (Question 7)

Potential customers for approaching loans were defined as those age groups where the **age average inquiry is more than 7.5**.

#### C. LTV Scoring and Promotions (Question 8)

This involved a DAX calculation and conditional logic for promotions:

1.  **LTV Score Measure:** A complex DAX measure was created based on the formula provided:
    $$\text{LTV} = (0.3 \times \text{Avg. Annual Income}) - (0.15 \times \text{Avg. Days in Delay}) + (0.4 \times \text{Avg. Credit Score}) + (0.075 \times \text{Avg. Amount Invested}) + (0.075 \times \text{Avg. Monthly Balance})$$
2.  **Promotional Tiers (DAX Logic):** A calculated field classified customers based on LTV:
    * $\mathbf{LTV > 80000}$: "30% off on online purchases + home loan at 4% interest"
    * $\mathbf{LTV \in [60000, 80000]}$: "15% off on online purchases + 10000 worth gift hampers"
    * $\mathbf{LTV \in [50000, 60000]}$: "Any loan at 5% interest rate"

### 3. Relationship and Trend Analysis (Questions 2, 5, 9, 10)

| Requirement | Visualization & Analysis | Value Provided |
| :--- | :--- | :--- |
| **Age vs. Credit Limit Change (Q2)** | **Scatter Plot** or **Line Chart** to analyse the correlation between customer age and credit limit adjustments. | Helps in tailoring credit products and strategies based on age demographics. |
| **Payment Behaviour by Credit Mix (Q5)** | **Matrix/Clustered Bar Chart** to examine the frequency of payment behaviours across different credit mix categories. | Provides insights into payment behaviour trends for risk management. |
| **Loans & Credit Cards by Age (Q9)** | **Line Chart** presenting the average number of loans and credit cards held by customers across different age groups. | Uncovers trends in credit card usage to inform targeted offers and marketing strategies. |
| **Count of Loan Types (Q10)** | **Bar Chart** showing the count of each type of loan dispersed. | Helps the company keep a record of the most popular loans and roll out offers accordingly. |

---

## 🚀 Getting Started

1.  **Download:** Clone this repository and download the `Project_1.pbix` file.
2.  **Power BI Desktop:** Open the file using Microsoft Power BI Desktop.
3.  **Explore:** Navigate through the report pages to review the visual insights corresponding to the client's requirements.
2.  **Power BI Desktop:** Open the file using Microsoft Power BI Desktop.
3.  **Explore:** Navigate through the report pages to review the visual insights corresponding to the client's requirements.
