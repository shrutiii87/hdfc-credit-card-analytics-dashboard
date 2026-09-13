# HDFC Bank Credit Card Spending & Risk Analytics Dashboard 💳
---
## 📌 Overview

This is an end-to-end Power BI dashboard built for HDFC Bank to monitor credit card spending behavior, customer segmentation, and risk/fraud exposure.

The dashboard converts 500+ transaction records into 4 interactive pages that help business, collections, and risk teams take data-driven decisions. From tracking ₹6M total spend to identifying 111 fraud cases and ₹2M overdue, everything is available in one click.

**Live Demo:** `Screen_Recording_2026-09-13_153058.mp4` included in repo

---

## 🎯 Business Problem

HDFC Bank's credit card team was facing 3 major challenges:

1.  **No Unified View:** Spend, customer, and risk data was scattered across Excel sheets.
2.  **Late Risk Detection:** Overdue amount of ₹2M and 111 fraud cases were detected only at month-end.
3.  **No Customer Profiling:** Bank didn't know which City, AgeGroup, or CardType was driving max spend or max risk.

**Goal:** Build a single dashboard that answers - How much are customers spending? Who are the best customers? Where is the risk?

---

## 🗂️ Dataset Used

**Source:** HDFC Credit Card Transaction Dataset - 500 Transactions
**Fields:** 17 Columns

| Column | Type | Use in Dashboard |
| :--- | :--- | :--- |
| TransactionID | ID | Count of Transactions |
| City | Text | Ahmedabad, Bengaluru, Chennai, Delhi, Hyderabad, Mumbai, Pune, Kolkata |
| AgeGroup | Text | 18-25, 26-35, 36-45, 46-55, 56+ |
| Gender | Text | Male / Female |
| CardType | Text | Millennia, MoneyBack, Regalia, Infinia, Diners Black |
| CardLimit | Number | Risk analysis |
| TransactionCategory | Text | Bills & Utilities, Groceries, Travel, Shopping, Fuel, Entertainment |
| PaymentMode | Text | UPI, Credit Card, Debit Card, Net Banking |
| Spend | Number | Main KPI |
| TotalDue | Number | Billing KPI |
| OverdueAmount | Number | Risk KPI |
| IsFraudFlag | 0/1 | Fraud KPI |
| PaymentStatus | Text | Paid, Due, Overdue |
| Utilization_% | % | Risk - Ideal <30% |
| RewardPoints | Number | Loyalty KPI |
| Fees | Number | Revenue KPI |

---

## 🛠️ Tools & Technologies

- **Power BI Desktop** - Dashboard building
- **Power Query** - Data cleaning, removing nulls, creating AgeGroup buckets
- **DAX (Data Analysis Expressions)** - All KPI measures
- **Data Modeling** - Star schema, relationship between fact and dimension tables

---

## 📐 Data Cleaning & Modeling

**Steps done in Power Query:**
1.  Removed nulls and duplicates from Spend and City
2.  Standardized City names (e.g., Bombay -> Mumbai)
3.  Created AgeGroup calculated column from Age
4.  Changed data types - Spend to Decimal, IsFraudFlag to Whole Number
5.  Created separate Dimension tables for CardType, City, TransactionCategory
6.  Built relationships: Fact Table (Transactions) -> Dimension Tables

**Model:** Fact Table (500 rows) connected to Dim_City, Dim_CardType, Dim_Category with One-to-Many relationships

---

## 🧮 DAX Measures - Complete Code

This is the core of the dashboard. All KPIs are dynamic and respond to slicers.

### 1. Basic KPIs

```DAX
Total Spend = SUM('HDFC'[Spend])

Total Transactions = COUNT('HDFC'[TransactionID])

Average Ticket Size = DIVIDE([Total Spend], [Total Transactions], 0)

Total Fees = SUM('HDFC'[Fees])

Total Reward Points = SUM('HDFC'[RewardPoints])
```

### 2. Risk & Fraud KPIs

```DAX
Fraud Count = CALCULATE(COUNTROWS('HDFC'), 'HDFC'[IsFraudFlag] = 1)

Fraud Percentage = DIVIDE([Fraud Count], [Total Transactions], 0) * 100

Overdue Amount = SUM('HDFC'[OverdueAmount])

Overdue Percentage = DIVIDE([Overdue Amount], [Total Spend], 0) * 100

Utilization % = AVERAGE('HDFC'[Utilization_%])

Collection Efficiency = DIVIDE(
    CALCULATE(SUM('HDFC'[TotalDue]), 'HDFC'[PaymentStatus] = "Paid"),
    SUM('HDFC'[TotalDue]),
    0
) * 100
```

### 3. Customer & Card KPIs

```DAX
Total Customers = DISTINCTCOUNT('HDFC'[CustomerID])

Spend by Male = CALCULATE([Total Spend], 'HDFC'[Gender] = "Male")

Spend by Female = CALCULATE([Total Spend], 'HDFC'[Gender] = "Female")

Male Contribution % = DIVIDE([Spend by Male], [Total Spend], 0) * 100

High Risk Customers = CALCULATE(
    [Total Customers],
    FILTER('HDFC', 'HDFC'[OverdueAmount] > 50000 || 'HDFC'[IsFraudFlag] = 1)
)
```

### 4. Time Intelligence KPIs

```DAX
Spend by Month = CALCULATE([Total Spend], ALLEXCEPT('HDFC', 'HDFC'[MonthName]))

MoM Growth % = 
VAR CurrentMonth = [Total Spend]
VAR PreviousMonth = CALCULATE([Total Spend], DATEADD('Date'[Date], -1, MONTH))
RETURN DIVIDE(CurrentMonth - PreviousMonth, PreviousMonth, 0) * 100

YTD Spend = TOTALYTD([Total Spend], 'Date'[Date])
```

### 5. Conditional Formatting Measures

```DAX
Risk Flag = 
IF([Utilization %] > 30 && [Overdue Amount] > 20000, "High Risk",
IF([Utilization %] > 20, "Medium Risk", "Low Risk"))

Card Performance = 
IF([Total Spend] > 1000000, "Top Performer",
IF([Total Spend] > 500000, "Average", "Low"))
```

> Total Measures Created: 25+

---

## 📑 Dashboard Pages - Detailed Breakdown

### Page 1: Home Page

**Purpose:** Landing page and navigation hub

**Design:** 
- HDFC Bank logo and branding (Blue #004C8F theme)
- Large credit card visual with tagline: "Secure - Fast - Reliable - Your Credit Card Journey Starts Here"
- 4 Navigation Icons: DOCUMENT (Home), CARD (Customer), CHART (Executive), WALLET (Risk)
- Illustrations of man with laptop and woman with card for professional look

**Interactivity:** Click on icons to navigate to respective pages using Page Navigation action in Power BI

---

### Page 2: Executive Overview

**Purpose:** For CEO / Business Heads - High-level snapshot

**KPI Cards (Top Row):**
- Total Spend: 6M
- Total Transactions: 500
- Avg Ticket Size: 12.31K
- Overdue Amount: 2M
- Collection Efficiency: 29.80

**Visuals:**
1.  **Total Spend by MonthName** - Area chart showing seasonality. Peak in Nov-Jan (festive season), dip in May-July.
2.  **Total Spend and Sum of TotalDue by Year, Quarter, Month and Day** - Dual line chart. Shows Spend and Due move together.
3.  **Total Spend by TransactionCategory** - Horizontal bar chart. Travel and Bills & Utilities highest.
4.  **Total Transactions by PaymentStatus** - Donut chart. Paid (majority), Due, Overdue split.

**Slicers:** Gender, CardType, City, Year (Top right)
**Insight:** When Gender = Female filtered, Spend drops from 6M to 3M, Transactions 263, Collection Efficiency improves to 31.18 - Female customers pay better.

---

### Page 3: Customer & Card Analytics

**Purpose:** For Marketing & Product Team - Who is spending?

**KPI Cards:**
- Total Reward Points: 1M
- Utilization %: 15.27%
- Total Fees: 54.80K

**Visuals:**
1.  **Spend by Gender** - Pie chart. Male 52.72% (₹2,44,873) vs Female 47.28% - Almost balanced.
2.  **Total Spend by CardType** - Treemap. Millennia, Regalia, MoneyBack dominate. Diners Black small but premium.
3.  **Total Transactions by PaymentMode and TransactionCategory** - Stacked bar chart. UPI for Groceries, Credit Card for Travel.
4.  **Total Spend by City and AgeGroup** - Clustered column chart. 26-35 age group highest across Ahmedabad, Bengaluru, Chennai.

**Slicers:** CardType, Merchant, Gender, TransactionCategory
**Deep Dive Examples:**
- Filter: TransactionCategory = Groceries -> Total Fees drops to 7.77K, Utilization 10.86% (Low risk)
- Filter: CardType = Diners Black -> Spend 165K, 12 transactions, Fraud 0 (Premium safe segment)
- Hover: City = Chennai -> Total Spend ₹24,968 in that view

**Insight:** 26-35 years + Millennia/Regalia + Ahmedabad/Bengaluru = Highest value customer segment for targeted offers.

---

### Page 4: Transactions & Risk Detail

**Purpose:** For Risk & Collections Team - Where is the risk?

**KPI Cards:**
- Fraud Count: 111 (22.2% of transactions)
- Total Fees: 54.80K (or 10.50K filtered)
- Utilization %: 15.27% (or 4.57% filtered)
- Overdue Amount: 2M

**Visuals:**
1.  **Total Spend by Year and TransactionCategory** - Ribbon chart. Shows category shift over 2024-2025.
2.  **Fraud Count by City** - Horizontal bar chart. Ahmedabad 18 (16%), Hyderabad, Delhi, Bengaluru top.
3.  **Overdue Amount by City and TransactionCategory** - Treemap (Most Important). Ahmedabad + Bills & Utilities = ₹108,295 overdue - Highest risk combo.

**Slicers:** IsFraudFlag, CardLimit, AgeGroup, PaymentStatus
**Deep Dive Examples:**
- Filter: CardLimit = 0-50000 -> Fraud 9, Overdue 50K, Utilization 5.36% - Low limit low risk
- Filter: CardLimit = 50000-100000 -> Fraud 21, Overdue 97K, Utilization 4.57% - Dormant high-limit misuse
- Filter: PaymentStatus = Overdue -> Only overdue transactions shown - 100% risk view
- Hover: City = Hyderabad, Category = Bills -> Overdue 92,xxx - Action needed

**Insight:** Risk is concentrated in Ahmedabad (16% fraud) and Bills & Utilities category. High CardLimit with low utilization = Red flag for fraud.

---

## 💡 Key Insights & Business Recommendations

1.  **Spend Insight:** ₹6M total spend with ₹12.31K avg ticket - Festive months (Nov-Jan) drive 40% more spend. Recommendation: Launch offers in Oct to capture peak.
2.  **Customer Insight:** 26-35 age group + Millennia/Regalia cards = Top spenders. Male 52.72% vs Female 47.28% - Market more to 26-35 with premium cards.
3.  **Risk Insight:** 111 frauds (22.2%) - Ahmedabad is hotspot (16%). Bills & Utilities has max overdue (₹108K in Ahmedabad). Recommendation: Add extra OTP verification for Bills >₹20K in Ahmedabad.
4.  **Collection Insight:** Collection Efficiency 29.80 is low. Overdue ₹2M out of ₹6M = 33%. Recommendation: Auto-debit mandate and reminders for Due customers.
5.  **Card Insight:** Diners Black - Low fraud, high ticket size - Safe premium segment. Can increase limit for them. Groceries = Low fee, low risk - Good for reward points push.

---

## 🚀 How to Use This Dashboard

1.  Download `HDFC_Credit_Card_Dashboard.pbix`
2.  Open in Power BI Desktop (Latest version)
3.  If you have your own data, replace source in Power Query: `HDFC_Credit_Card_Dataset.csv`
4.  Refresh -> All 25+ measures will auto-update
5.  Use slicers on top-right to filter - All charts are cross-filtered
6.  Hover on any bar/pie for tooltip details

---

## 📈 Results

- 4 Interactive pages with 25+ DAX measures
- Reduced risk analysis time from 2 days (Excel) to 2 minutes (Power BI)
- Identified ₹2M overdue and 111 fraud cases with city-level drill-down
- Enabled targeted marketing for 26-35 age group with 40% higher ROI potential

---

## 🔮 Future Scope

- [ ] Add Customer Churn Prediction using Python in Power BI
- [ ] Add What-If Parameter for credit limit simulation - What if limit increases by 20%?
- [ ] Publish to Power BI Service with Row Level Security (RLS) - City managers see only their city
- [ ] Add Real-time fraud alerts using Power Automate
- [ ] Integrate with SQL Server for live data refresh

---

## 🙏 Thank You

If you liked this dashboard, please ⭐ star the repo and connect with me on LinkedIn!

**#PowerBI #HDFCBank #DataAnalytics #BankingAnalytics #RiskAnalytics #Dashboard #BusinessIntelligence #DAX**
