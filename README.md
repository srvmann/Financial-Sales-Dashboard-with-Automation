# Financial-Sales-Dashboard-with-Automation
A Power BI-centric solution that transforms a manual, error-prone financial data workflow into an automated, cost-efficient pipeline, delivering key customer segmentation and Lifetime Value (LTV) insights to the end User.

---
# 🏆 US Financial Data Analysis – Power BI Project

## 📘 Project Overview
This Power BI project automates a previously manual, error-prone workflow for the U.S. government’s financial dataset.  
The solution integrates **automation, ETL, and advanced analytics** to deliver actionable insights on customer segmentation and **Lifetime Value (LTV)** scoring.

---

## 🎯 Objectives
- Automate ingestion and transformation of ~25 daily CSV files.
- Eliminate manual data handling and minimise human errors.
- Provide customer segmentation insights based on credit behavior.
- Develop an LTV model to support data-driven promotional decisions.

---

## ⚙️ Data Pipeline & Automation Workflow

**Tools & Technologies Used:**  
`Microsoft Outlook`, `Power Automate`, `Python (google-auth, pandas)`, `Google Drive API`, `Power BI`, `Power Query (M Language)`

### Workflow Summary
1. **Email Standardization:**  
   All survey teams include **“Credit Score”** in the email subject line.
2. **Email Filtering:**  
   Emails automatically move into a dedicated folder via rules.
3. **Power Automate Integration:**  
   Power Automate monitors the inbox folder and uploads attachments to **Google Drive**.
4. **Data Consolidation (Python):**  
   A Python script reads all Google Drive files and combines them into a single dataset (`combined_df.csv`).
5. **Power BI Connection:**  
   Power BI connects to the consolidated file for **daily refresh** {we can automate that as well from the workspace if we have paid account}.

> 💡 *Manual task remaining:* Deleting outdated daily data from Google Drive to manage storage.

---

## 🧹 Data Transformation (Power Query)

Performed in **Power Query (M)** before loading into the Power BI data model.

### Key Steps
- **File Combination:** Merged all individual datasets into one master table.  
- **Credit History Cleaning:** Replaced invalid or negative entries in `Num_Bank_Accounts` using the column median.  
- **Loan Type Counting:** Counted distinct loan types in delimited strings.  
- **Credit Age Conversion:** Transformed text-based credit history (e.g., “X Years and Y Months”) into numeric months.

---

## 📊 Analytical Insights & DAX Highlights

### 1. Core KPIs
| Metric | Formula Type | Purpose |
|:--|:--|:--|
| Avg Annual Income | `AVERAGE` | Income distribution overview |
| Avg Monthly Balance | `AVERAGE` | Spending and savings trend |
| Avg Delay in Payment | `AVERAGE` | Credit discipline assessment |
| Avg Credit Utilisation | `AVERAGE` | Credit risk and utilization measure |

### 2. Customer Segmentation
Created DAX measures to segment customers by **age group** and flag **potential customers** based on credit inquiries.

```dax
Potential Customer = 
VAR customer = AVERAGEX(
    FILTER(
        combined_df,
        NOT(ISERROR(VALUE(combined_df[Custom_Num_Credit_Inqueries])))
    ),
    VALUE(combined_df[Custom_Num_Credit_Inqueries])
)

### 3. LTV Scoring

Calculated **Customer Lifetime Value** to recommend tailored promotional offers.

**LTV Formula:**
[
LTV = (0.3 \times \text{Avg Income}) - (0.15 \times \text{Avg Delay}) + (0.4 \times \text{Credit Score}) + (0.075 \times \text{Avg Invested}) + (0.075 \times \text{Avg Balance})
]

**DAX Implementation:**

```dax
LTV Score = 
VAR LTV = (
    (0.3 * average_annual_income) -
    (0.15 * average_delay_in_payment) +
    (0.4 * Credit_Score) + 
    (0.075 * average_amount_invested) + 
    (0.075 * average_monthly_balance)
)
RETURN
IF(LTV > 80000, "80% off + Home Loan @ 4%",
    IF(LTV > 60000 && LTV < 80000, "15% off + Gift Hampers",
        IF(LTV > 50000 && LTV <= 60000, "Any Loan @ 5%", BLANK())
    )
)
```

---

## 📈 Visual Insights

| Visualization                      | Insight                                                   |
| :--------------------------------- | :-------------------------------------------------------- |
| **Age vs. Credit Limit**           | Correlation between customer age and credit limit changes |
| **Payment Behavior by Credit Mix** | Risk segmentation across credit types                     |
| **Loans & Cards by Age**           | Average count of financial products per age group         |
| **Loan Type Distribution**         | Identifies popular loan categories for targeted campaigns |

---

## 🧠 Key Outcomes

✅ Fully automated ETL pipeline with zero manual intervention (except cleanup).
✅ Accurate, timely reporting through daily cloud refresh.
✅ Enhanced customer segmentation and risk profiling.
✅ Actionable LTV-based promotional strategies for better ROI.

---


## 🧩 Tools & Technologies

* **Power BI**
* **Power Query (M Language)**
* **Python**
* **Power Automate**
* **Google Drive API**
* **Microsoft Outlook**

---

## 🏁 Conclusion

This project showcases a **complete automation-to-insight workflow**, combining data engineering, automation, and analytics in a single Power BI solution.
It stands as a scalable framework for any organization looking to automate reporting and derive value-driven insights from large, multi-source datasets.

---

## 👤 Author

**Saurav Kumar**
📍 Delhi, India
🔗 [LinkedIn](https://www.linkedin.com/in/sauravkumaar/) • [GitHub](https://github.com/srvmann) • [Portfolio](https://www.datascienceportfol.io/thisissauurav)

```

---
2. Or generate a **PDF version** formatted for your portfolio (with branding and visuals)?
```
