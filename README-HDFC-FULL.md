<img width="1200" height="420" alt="hdfc-bank-credit-card-analytics-header" src="https://github.com/user-attachments/assets/d7ac7691-d839-41a1-bde5-2f7d4f7d96d1" />

---

## 🎯 Objective

<img width="1600" height="1000" alt="hdfc-dashboard-main" src="https://github.com/user-attachments/assets/eba98a6a-598a-47d8-9c39-e0c9da181c94" />

To build a comprehensive, end-to-end **HDFC Bank Credit Card Spending & Risk Analytics Dashboard** in Power BI that enables the bank to track spending behavior, understand customer segmentation, and monitor fraud & overdue risk in real-time. The goal is to convert raw credit card transactional data into a **Secure, Fast, and Reliable** decision-making tool for business, collections, and risk teams.

---

## 📄 Problem Statement

You are hired as a **Junior Data Analyst** working on the HDFC Bank Credit Card analytics team. The bank holds a **Credit Card Transaction dataset** of 500+ customers and wants a unified dashboard that can answer critical business questions around spend, customer value, and risk.

Your manager asks you to build a 4-page interactive Power BI dashboard with advanced DAX, Power Query cleaning, and cross-filtering to deliver actionable insights and recommend business actions for spend growth and risk mitigation.

The dataset contains:

- **Customer attributes** — AgeGroup, Gender, City, CardType, CardLimit, Reward Points
- **Transaction attributes** — TransactionCategory, PaymentMode, Spend, Total Due, Fees, PaymentStatus
- **Risk attributes** — Overdue Amount, IsFraudFlag, Utilization %, Collection Efficiency

---

<img width="1400" height="900" alt="hdfc-pages-overview" src="https://github.com/user-attachments/assets/56ac87b6-7a61-4f3a-ac71-188d70ab46da" />

---

# 📂 Project Files

| 📄 File / Folder | 📌 Description |
|------------------|----------------|
| 📊 `HDFC_Credit_Card_Dashboard.pbix` | Main Power BI file — complete data model, DAX measures & all 4 dashboard pages |
| 📊 `HDFC_Credit_Card_Dataset.csv` | Raw credit card transaction dataset (500 records) |
| 📑 `HDFC_Bank_Dashboard_Analysis_Report.docx` | Final analysis report — KPIs, customer insights, fraud/risk diagnostics, business recommendation |
| 📘 `README.md` | Project documentation and workflow guide |

---

## 🛠 Tools Used

<div>

<img src="https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black"/>
<img src="https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoft&logoColor=white"/>
<img src="https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white"/>
<img src="https://img.shields.io/badge/Data%20Modeling-EC4899?style=for-the-badge"/>
<img src="https://img.shields.io/badge/Data%20Visualization-059669?style=for-the-badge"/>
<img src="https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white"/>
<img src="https://img.shields.io/badge/Banking%20Analytics-0F172A?style=for-the-badge"/>
<img src="https://img.shields.io/badge/Risk%20Analytics-FF6B6B?style=for-the-badge"/>
<img src="https://img.shields.io/badge/KPI%20Analysis-F59E0B?style=for-the-badge"/>

</div>

---

## 🎬 Project Demo

[![Watch Demo](https://img.shields.io/badge/Watch%20Demo-Add%20Your%20Link-blue?style=for-the-badge&logo=googledrive&logoColor=white)](https://drive.google.com/file/d/1oD4nGN8-yN_oPSTUD4Knz48nX6V0lk5o/view?usp=sharing)

📹 Add a link to your project walkthrough video here - `Screen_Recording_2026-09-13_153058.mp4`

---

### 🧬 Dataset Structure — HDFC Credit Card Dataset

| Field Name | Data Type | Description | Notes |
|------------|-----------|-------------|-------|
| `TransactionID` | Integer | Unique identifier for each transaction | Not used as a KPI |
| `CustomerID` | Integer | Unique identifier for each customer | Used for distinct count |
| `City` | String | City of customer - Ahmedabad, Bengaluru, Chennai, Delhi, Hyderabad | Slicer + Fraud/Risk analysis |
| `AgeGroup` | String | 18-25, 26-35, 36-45, 46-55, 56+ | Used in Customer Analytics |
| `Gender` | String | Male / Female | Spend by Gender |
| `CardType` | String | Millennia, MoneyBack, Regalia, Infinia, Diners Black, etc. | Spend by CardType - strongest business driver |
| `CardLimit` | Integer | Credit limit assigned to customer | Risk analysis - limit vs utilization |
| `TransactionCategory` | String | Bills, Groceries, Travel, Shopping, Fuel, Entertainment | Core dimension |
| `PaymentMode` | String | UPI, Credit Card, Debit Card, Net Banking | Used in breakdown |
| `Spend` | Float | Transaction spend amount | 🎯 **Main KPI** |
| `TotalDue` | Float | Total due amount for the period | Used in due analysis |
| `OverdueAmount` | Float | Overdue amount pending | 🎯 **Risk KPI** |
| `IsFraudFlag` | Binary Int | 1 = Fraud, 0 = Not Fraud | Fraud Count calculation |
| `PaymentStatus` | String | Paid / Due / Overdue | Payment donut chart |
| `Utilization_%` | Float | Card utilization % | Risk metric - ideal <30% |
| `RewardPoints` | Integer | Reward points earned | Customer loyalty |
| `Fees` | Float | Total fees charged | Revenue metric |

---

<img width="1200" height="420" alt="partb" src="https://github.com/user-attachments/assets/ce454308-3e85-4d11-b748-1043655ae055" />

## 🧠 Part B : Dataset Understanding & Preparation

### 7⃣ Identify independent and dependent variables / KPIs

```DAX
Independent Dimensions = [City], [AgeGroup], [Gender], [CardType], [TransactionCategory], [PaymentMode]
Dependent KPIs = [Total Spend], [Overdue Amount], [Fraud Count], [Utilization %], [Collection Efficiency]
```

💡 **Insight:** City, CardType and TransactionCategory are the independent dimensions; Spend, Overdue and Fraud are the dependent KPIs. All KPIs are numeric, so DAX measures are used for aggregation, no encoding needed. 🎯

---

### 8⃣ Visualize relationships between dimensions and KPIs

```DAX
Total Spend = SUM('HDFC'[Spend])
Total Overdue = SUM('HDFC'[OverdueAmount])
Fraud Count = COUNTROWS(FILTER('HDFC', 'HDFC'[IsFraudFlag]=1))
```

💡 **Insight:** Bar and area charts show Travel & Bills & Utilities drive highest spend, while Ahmedabad (16%) & Bengaluru show higher fraud concentration — confirming City and Category carry strong business and risk signal. 📊

---

### 9⃣ Data Cleaning & Modeling in Power Query

```m
let
    Source = Csv.Document(File.Contents("HDFC_Credit_Card_Dataset.csv")),
    #"Removed Nulls" = Table.SelectRows(Source, each [Spend] <> null),
    #"Changed Type" = Table.TransformColumnTypes(#"Removed Nulls", {{"Spend", type number}, {"City", type text}}),
    #"Created AgeGroup" = Table.AddColumn(#"Changed Type", "AgeGroup", each if [Age] < 25 then "18-25" else if [Age] < 35 then "26-35" else "36-45")
in
    #"Created AgeGroup"
```

💡 **Insight:** Cleaned 500 rows with no nulls — created calculated columns for AgeGroup, standardized City/CardType, and built a star schema with dimension and fact separation for reliable slicing. 🔀

---

<img width="1200" height="420" alt="partC" src="https://github.com/user-attachments/assets/635779b6-71a9-4362-960e-ba5712cf0dd2" />

## 📊 Part C : Home Page & Executive Overview

### 🔟 Implement Home Page - Entry Point

```DAX
Home Page Navigation = DOCUMENT | CARD | CHART | WALLET
```

**Output:** Clean landing page with HDFC branding, navigation buttons to Executive Overview, Customer & Card Analytics, and Transactions & Risk Detail

💡 **Insight:** Home page acts as a control center - reduces cognitive load and provides guided navigation, similar to a banking app UX. 📐

---

### 1⃣1⃣ Implement Executive Overview KPIs

```DAX
Total Spend = SUM(HDFC[Spend]) // 6M
Total Transactions = COUNT(HDFC[TransactionID]) // 500
Avg Ticket Size = DIVIDE([Total Spend], [Total Transactions]) // 12.31K
Overdue Amount = SUM(HDFC[OverdueAmount]) // 2M
Collection Efficiency = DIVIDE([Paid Amount], [Total Due]) // 29.80
```

**Output:** KPI Cards: Total Spend 6M · Total Transactions 500 · Avg Ticket Size 12.31K · Overdue Amount 2M · Collection Efficiency 29.80

💡 **Insight:** Total Spend of ₹6M with 500 transactions gives Avg Ticket Size of ₹12.3K — healthy spend pattern but 2M overdue signals collections team needs focus. Collection Efficiency at 29.80 shows room for improvement. 📏

---

### 1⃣2⃣ Validate Spend Trends and Payment Behavior

```DAX
Spend by Month = Area Chart with MonthName on X-Axis, Total Spend on Y-Axis
Payment Status = Donut Chart with Paid vs Due vs Overdue
```

💡 **Insight:** Monthly spend shows peaks in Nov-Jan and dips in mid-year — TotalDue closely follows spend, indicating consistent billing cycle. Donut shows majority Paid, with small but critical Overdue slice (500 total). ✅

---

<img width="1200" height="420" alt="partD" src="https://github.com/user-attachments/assets/4eebf419-bfb4-4188-a545-912c7d329d" />

## 📈 Part D : Customer & Card Analytics

### 1⃣3⃣ Evaluate Customer Segmentation KPIs

```DAX
Total Reward Points = SUM(HDFC[RewardPoints]) // 1M
Utilization % = AVERAGE(HDFC[Utilization_%]) // 15.27%
Total Fees = SUM(HDFC[Fees]) // 54.80K
```

**Output:** Reward Points 1M · Utilization 15.27% · Total Fees 54.80K

💡 **Insight:** Utilization at 15.27% is in safe zone (<30% ideal), but fees of 54.8K show revenue opportunity from high-utilization customers. Reward points of 1M indicates strong loyalty program engagement. 📉

---

### 1⃣4⃣ Interpret Spend by Gender, CardType, City & AgeGroup

- **Spend by Gender** — Male 52.72% (₹2,44,873) vs Female 47.28% — balanced but male slightly higher
- **Spend by CardType** — Millennia & Regalia drive max spend, Diners Black for premium segment
- **Spend by City & AgeGroup** — Chennai (₹24,968), Ahmedabad high spend, 26-35 AgeGroup most active across all cities

---

### 1⃣5⃣ Implement Interactive Slicers for Customer View

```DAX
Slicers Used = Gender, CardType, Merchant, TransactionCategory, City, AgeGroup
```

**Output:** When filtered for Merchant = Groceries, Total Fees drops from 54.80K to 7.77K, Utilization drops to 10.86% - proving grocery transactions are low-risk, low-fee

💡 **Insight:** Slicers prove behavior changes by category - Groceries = low risk, Travel = high spend high fee. This helps in targeted card offers. 📍

---

<img width="1200" height="420" alt="partE" src="https://github.com/user-attachments/assets/572664aa-80b6-4141-80f2-5e49688032b8" />

## 📉 Part E : Transactions & Risk Detail

### 1⃣6⃣ Implement Fraud & Overdue Risk Analysis

```DAX
Fraud Count = COUNTROWS(FILTER(HDFC, HDFC[IsFraudFlag]=1)) // 111
Fraud % = DIVIDE([Fraud Count], [Total Transactions]) // 22.2%
Overdue by City = SUMMARIZE(HDFC, HDFC[City], "Overdue", SUM(HDFC[OverdueAmount]))
```

**Output:** Fraud Count 111 (22.2%) · Ahmedabad 16% of fraud · Hyderabad, Delhi, Bengaluru next

💡 **Insight:** Fraud Count 111 with 16% from Ahmedabad — Bills & Utilities category shows highest overdue exposure (₹108,295 in Ahmedabad alone), needs stricter verification and OTP. 🚀

---

### 1⃣7⃣ Explain why Risk Analysis is Critical

💡 **Insight:** Risk analysis is critical because spend alone doesn't show bank health — overdue amount (2M) and fraud (111) directly impact profitability. By breaking overdue by City & TransactionCategory using Treemap, bank can identify that Ahmedabad + Bills & Utilities is the riskiest combo.

---

<img width="1200" height="420" alt="partF" src="https://github.com/user-attachments/assets/c3475261-7f6b-4c72-bb0d-5f5cc5284643" />

## 🔁 Part F : DAX Measures & Data Modeling

### 1⃣8⃣ Implement Core DAX Measures (From Scratch)

```DAX
Total Spend = SUM(HDFC[Spend])
Total Transactions = COUNT(HDFC[TransactionID])
Avg Ticket Size = DIVIDE([Total Spend], [Total Transactions])
Collection Efficiency = DIVIDE([Total Paid], [Total Due]) * 100
Fraud Count = CALCULATE(COUNTROWS(HDFC), HDFC[IsFraudFlag]=1)
Utilization % = AVERAGE(HDFC[Utilization_%])
Overdue Amount = SUM(HDFC[OverdueAmount])
```

**Coefficients / Outputs:** Total Spend 6M, Overdue 2M, Avg Ticket 12.31K - similar to how MLR coefficients showed impact of each feature

💡 **Insight:** DAX measures are the backbone - unlike Simple Linear Regression that uses only area, these measures combine multiple dimensions to give true business picture. 〰

---

### 1⃣9⃣ Compare Filtered vs Unfiltered View

| Filter Applied | Total Spend | Total Transactions | Avg Ticket Size | Fraud Count | Insight |
|----------------|-------------|--------------------|-----------------|-------------|---------|
| No Filter (All) | 6M | 500 | 12.31K | 111 | Baseline |
| Gender = Female | 3M | 263 | 12.34K |  - | Female contributes 47% |
| CardType = Diners Black | 165K | 12 | 13.83K | 0 | Premium but low fraud |
| Transaction = Groceries | 2M | 130 | 10.86% Util | 21 | Low risk, low fee |

💡 **Insight:** Filtered vs unfiltered view is like comparing SLR vs MLR — single filter (Gender) shows partial picture, combined filters (City + CardType + Category) show true risk, just like MLR uses multiple features. ➖

---

### 2⃣0⃣ Identify Signs of High Risk / Low Collection

**Output:** When CardLimit = 50K-100K, Fraud Count = 21, Overdue = 97K, Utilization = 4.57% — High Limit but Low Utilization indicates dormant high-limit cards being misused

💡 **Insight:** High CardLimit + Low Utilization + High Fraud = Red Flag. Similar to overfitting detection - gap between expected behavior (high limit should mean high spend) and actual behavior (low utilization but high fraud) signals anomaly. ⚖

---

<img width="1200" height="420" alt="partG" src="https://github.com/user-attachments/assets/4d3ede3a-6903-488a-a924-698ec0c5f388" />

## ⚙ Part G : Interactivity & Slicer Optimization

### 2⃣1⃣ Explain Interactivity Conceptually

Interactivity in Power BI is like Gradient Descent optimization - it starts with initial view (all data) and repeatedly updates visuals in the direction that reduces information overload, with slicers controlling step size: **initial load → user selects filter → cross-filter visuals → compute new KPIs → update charts → repeat.**

---

### 2⃣2⃣ – 2⃣4⃣ Implement Slicer Interactions (Batch, Single, Multi-Select)

```DAX
// Batch Filtering - All cities at once
CALCULATE([Total Spend], ALL(HDFC[City]))

// Single Select - One city like Ahmedabad
CALCULATE([Total Spend], HDFC[City]="Ahmedabad")

// Multi-Select - Ahmedabad + Bengaluru
CALCULATE([Total Spend], HDFC[City] IN {"Ahmedabad", "Bengaluru"})
```

| Method | Final Result | Insight |
|--------|--------------|---------|
| 🟦 **Batch Filter (No Slicer)** | Total Spend 6M, Fraud 111 | Smoothest overview, lowest detail, but slow to find insights - one view for full dataset |
| 🟨 **Single Select Slicer** | Spend 626K, Transactions 50 | Reaches specific insight in few clicks, but view is noisy and total context is lost |
| 🟩 **Multi-Select Slicer** | Spend 97K, Transactions 7 | Matches Batch's stability with far less noise - best balance of overview and detail |

---

### 2⃣5⃣ Compare Interaction Behavior and Performance

| Method | Final Spend Shown | Time to Insight |
|--------|-------------------|-----------------|
| No Slicer (Full View) | 6M | 0.5s but too broad |
| Single City (Ahmedabad) | 97K | 0.2s fast but narrow |
| Multi City (Ahmedabad + Hyderabad) | 206K | 0.3s - best practical |

💡 **Insight:** No Slicer = fastest but needs more analysis; Single Slicer = fast insight but narrow; Multi-Slicer = the practical winner for business review. 🏆

---

<img width="1200" height="420" alt="partH" src="https://github.com/user-attachments/assets/3abee52b-4390-4780-a9f9-ed1e10ed0659" />

## 🔍 Part H : Business Insights & Risk Diagnostics

### 2⃣6⃣ Analyze Bias in Customer Data vs Actual Risk

```DAX
CV Analysis = Spend by City vs Fraud Count by City - Do they align?
```

| City | Total Spend | Fraud Count | Fraud % | Risk Level |
|------|-------------|-------------|---------|------------|
| Ahmedabad | High | 18 (16%) | High | High Risk - High Value |
| Bengaluru | High | 15 | Medium | Monitor |
| Chennai | Medium | Low | Low | Low Risk - Safe |
| Delhi | Medium | High | High | High Risk |

💡 **Insight:** Ahmedabad shows high spend AND high fraud - high bias towards risk. Chennai shows balanced spend with low fraud - low variance, most stable city. Ahmedabad needs stricter KYC, Chennai can get higher limit offers. ⚖

---

### 2⃣7⃣ How Dashboard Complexity Affects Decision Making

A dashboard that is **too simple** (one KPI) has high bias — both business and risk views stay hidden (underfitting). As complexity increases (more pages, more slicers, more DAX), bias falls and insight keeps improving. If the dashboard becomes **too complex** (too many charts on one page), it starts showing noise — variance rises, load time increases and decision time rises (overfitting). Total insight is maximized at the balance point between simplicity and detail.

---

### 2⃣8⃣ Identify the Best Page for Best Business Balance

| Page | Business Value | Risk Value | Balance Score |
|------|----------------|------------|---------------|
| Executive Overview | 0.85 | 0.60 | 0.72 |
| Customer & Card Analytics | 0.90 | 0.65 | 0.77 |
| Transactions & Risk Detail | 0.70 | 0.95 | **0.82 - Best Balanced** |

💡 **Insight:** Transactions & Risk Detail has both the best risk coverage and decent business coverage - the most consistent, best-generalizing page, similar to how MLR had smallest train-CV gap. 🥇

---

<img width="1200" height="420" alt="partI" src="https://github.com/user-attachments/assets/327f69f3-3396-4e74-94a6-03bc9736fa15" />

## 📊 Part I : Final Analysis & Reporting

### 2⃣9⃣ Final Report Summary

| ❓ Question | ✅ Answer |
|-------------|----------|
| Best-performing CardType and why? | **Millennia & Regalia** — Highest Total Spend and Reward Points, with moderate utilization (15%), because they cater to 26-35 high-spending age group |
| Impact of Slicers & DAX optimization? | No slicer gave 6M overview; Single City slicer drilled to 97K spend for Ahmedabad; Multi-slicer matched overview stability with targeted detail - best practical |
| Evidence of high risk / low collection? | Ahmedabad = 16% fraud + ₹108K overdue in Bills & Utilities; 50K-100K CardLimit = high fraud (21) + low utilization (4.57%) = dormant misuse |
| Practical business interpretation? | Spend depends on more than city - CardType, AgeGroup, TransactionCategory all affect risk, so bank can use Customer & Card Analytics as supporting tool for limit enhancement and fraud prevention |
| Final conclusion? | Transactions & Risk Detail is the best page overall; Multi-select slicer is the best interaction method for accuracy, speed and stability |

---

## 📂 Project Workflow

1. **Dataset Understanding** → Identify independent dimensions and dependent KPIs, visualize relationships
2. **Data Cleaning** → Power Query - Remove nulls, create AgeGroup, standardize City/CardType
3. **Data Modeling** → Build star schema, create dimension and fact tables
4. **DAX Measures** → Total Spend, Overdue, Fraud Count, Avg Ticket Size, Utilization %, Collection Efficiency
5. **Executive Overview** → KPI cards, Spend by Month, Spend vs Due, Payment Status Donut
6. **Customer & Card Analytics** → Gender, CardType, City & AgeGroup analysis, Reward Points & Fees
7. **Transactions & Risk Detail** → Fraud Count by City, Overdue by City & Category Treemap, Spend by Year & Category
8. **Interactivity & Optimization** → Single, Multi, Batch slicers, cross-filtering validation
9. **Final Reporting** → Best CardType, risk diagnostics, business interpretation, conclusion

---

## 📈 Results & Insights

- ✅ **Four dashboard pages** built and compared — Home, Executive Overview, Customer & Card Analytics, Transactions & Risk Detail
- ✅ **Transactions & Risk Detail** selected as best-balanced page — **Fraud 111**, Overdue 2M, Utilization 15.27%, Fees 54.8K with city-level breakdown
- ✅ **Three slicer methods** implemented — No Filter, Single Select, Multi-Select — Multi-Select identified as practical winner
- ✅ **Risk diagnostics** confirm Ahmedabad + Bills & Utilities is riskiest combo (₹108,295 overdue) while Chennai is safest
- ✅ **Business diagnostics** confirm Millennia & Regalia + 26-35 AgeGroup is highest value segment
- ✅ Final report delivered with KPI comparison, interactivity impact, risk diagnostics and business interpretation

---

## 📌 Expected Outcomes

- Understand how to **plan and execute a complete banking analytics dashboard workflow**
- Build and compare **Executive, Customer, and Risk dashboards** with intent, not habit
- Implement **DAX measures from scratch** and reason about the filter-context vs row-context trade-off
- Diagnose **high-risk customers, overdue patterns, and fraud concentration** using slicers and Treemaps
- Translate dashboard results into a **practical business recommendation for credit limit and fraud control**

---

## ⚙ Installation & Setup

```bash
# clone the repository
git clone https://github.com/yourusername/hdfc-credit-card-analytics-dashboard.git
cd hdfc-credit-card-analytics-dashboard

# No environment needed - Just open Power BI file
# 1. Install Power BI Desktop from Microsoft Store
# 2. Open HDFC_Credit_Card_Dashboard.pbix
# 3. Refresh data if you add new CSV
# 4. Interact with slicers

# For dataset preview
# Open HDFC_Credit_Card_Dataset.csv in Excel / Power BI
```

---

## 🚀 Future Scope

- [ ] Add **Customer Churn Prediction** using Python integration in Power BI
- [ ] Engineer features from `CardLimit`, `Utilization_%`, `RewardPoints` for credit scoring
- [ ] Add **What-If Parameter** for Credit Limit enhancement simulation
- [ ] Deploy dashboard to **Power BI Service** with scheduled refresh and Row Level Security (RLS)
- [ ] Add **Anomaly Detection** for real-time fraud alerts

---

## 🙏 Thank You

Thank you for taking the time to explore this project!
Your feedback, suggestions, and contributions are always welcome.

⭐ If you found this project helpful, don't forget to **star the repository** and share it with others.
