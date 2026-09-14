# HDFC Bank Credit Card Analytics Dashboard | Power BI Project 💳📊

![HDFC Bank](https://img.shields.io/badge/HDFC%20BANK-Credit%20Card%20Analytics-004C8F?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgaGVpZ2h0PSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij48cGF0aCBmaWxsPSJ3aGl0ZSIgZD0iTTEyIDJMNi41IDguNWgxM0wxMiAyWiIvPjwvc3ZnPg==)
![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Measures-blue?style=for-the-badge)
![Power Query](https://img.shields.io/badge/Power%20Query-ETL-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Project-Completed-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge)

---

## 📋 Table of Contents
- [Overview](#-overview)
- [Video Walkthrough](#-video-walkthrough)
- [Business Problem & Objective](#-business-problem--objective)
- [Dataset Details](#-dataset-details)
- [Dashboard Pages Deep Dive](#-dashboard-pages-deep-dive---from-video)
- [Design & UI - GitHub Template](#-design--ui---github-template)
- [DAX Measures Used](#-dax-measures-used)
- [Key Insights From Video](#-key-insights-from-video)
- [Tools & Technologies](#️-tools--technologies)
- [Project Structure](#-project-structure)
- [How to Run This Project](#-how-to-run-this-project)
- [Screenshots](#-screenshots)
- [Future Improvements](#-future-improvements)
- [Author & Connect](#-author--connect)

---

## 📌 Overview

This repository contains a complete **HDFC Bank Credit Card Analytics Dashboard** built in **Microsoft Power BI**. 

This is not a static dashboard. As you can see in the attached video `video_HDFC_working.mp4`, the entire dashboard is **fully interactive** - every KPI card, chart, and visual responds instantly to slicers. The project demonstrates end-to-end BI workflow: Data Cleaning -> Data Modeling -> DAX -> UI Design -> Interactive Visualizations.

The dashboard uses a **custom HDFC-themed background template** hosted on GitHub (`/assets` folder) to give it a professional banking look - light blue gradient, clean cards, HDFC logo, and illustrated characters.

This project is ideal for showcasing skills for **Data Analyst, Business Analyst, and Power BI Developer** roles in Banking and Finance domain.

---

## 🎬 Video Walkthrough

**File:** `video_HDFC_working.mp4` (1432805322067695)

The video shows 3 pages and live filtering:

1.  **0:00 - 14:00 sec - EXECUTIVE OVERVIEW:** You can see mouse hovering and selecting filters from the right-side filter pane. 
    - At 0:01, selects Gender, then CardType = Diners Black, Gold, Infinia etc. 
    - At 0:03, KPIs update from 6M / 500 Transactions to 3M / 263 Transactions.
    - At 0:06, selects City = Pune, Mumbai etc. and Total Spend drops to 626K / 50 Transactions.
    - At 0:09, selects Year = 2024, 2025, tooltip shows "2024 February Total Spend 1,23,456" etc.
    - Shows Area Chart animations and Donut chart for Payment Status (Due, Paid, Overdue).

2.  **14:00 - 39:00 sec - CUSTOMER & CARD ANALYTICS:**
    - Shows Pie chart for Spend by Gender, Treemap for Total Spend by CardType (Millennia is biggest block).
    - Hover shows tooltip: "Gender Male Total Spend 3,244,673 (52.72%)", "City Bengaluru Age 36-45 Total Spend 250,20" etc.
    - Left side slicers: TransactionCategory, Merchant, Gender. User filters TransactionCategory = Travel, Entertainment, etc.
    - User filters Merchant = Swiggy, GoIbibo etc.
    - User filters Gender = Male / Female. When Gender = Male selected alone, Treemap shows only Diners Black and Millennia, Total Reward Points becomes 1M, Utilization 14.87%, Total Fees 4.34K.
    - Bottom clustered column chart shows Total Spend by City and AgeGroup - dynamically filters to one city when selected.

3.  **39:00 - 76:00 sec - TRANSACTIONS & RISK DETAIL:**
    - Most critical page. Top KPIs: 111 Fraud Count, 54.80K Total Fees, 15.27 Utilization %, 2M Overdue Amount.
    - Visual 1: Ribbon Chart - Total Spend by Year and TransactionCategory. Shows rank changes: In 2024 Groceries was Rank 1, in 2025 Groceries Rank 3 with -17,249 change (-22.98%).
    - Visual 2: Funnel Chart - Fraud Count by City. Tooltip: "City Pune Fraud Count 20 Percent of first 100%". Then shows "City Bengaluru Fraud Count 18 Percent 90%", "City Delhi 5", "City Chennai TransactionCategory Fuel Overdue Amount 47,730".
    - Visual 3: Treemap - Overdue Amount by City and TransactionCategory.
    - Right-side filters: IsFraudFlag (0/1), CardLimit (100K to 1000000 range), AgeGroup (18-25 to 56+), PaymentStatus (Due, Overdue, Paid).
    - In video, user filters IsFraudFlag = 1, CardLimit range, AgeGroup 46-55, 56+, PaymentStatus = Due/Overdue, and all visuals filter instantly. At end, Fraud Count goes from 111 to 21 to 9 to 4 to 2 based on filters.

This video is the proof of interactivity.

---

## 🎯 Business Problem & Objective

**For HDFC Bank:**

1.  **Executive Level:** Leadership needs a one-page view of total business health - How much are customers spending? What is the average ticket size? What is the overdue amount and collection efficiency?
2.  **Customer Level:** Marketing team needs to know - Which gender spends more? Which card type (Regalia, Millennia, Infinia, Diners Black) is most profitable? Which cities and age groups are high spenders? What is the payment mode preference?
3.  **Risk Level:** Risk & Compliance team needs - Where is fraud concentrated city-wise? Which transaction category has highest overdue? What is the utilization % vs fees?

**Objective:** Build a single Power BI file that answers all 3 with interactive slicers.

---

## 🗂️ Dataset Details

**Source:** HDFC Credit Card Transaction Dataset (Synthetic / Anonymized for project)

**Rows:** 500 Transactions (can scale)

**Columns & Data Dictionary:**

| Column Name | Description | Example |
| :--- | :--- | :--- |
| TransactionID | Unique ID | TXN001 |
| Gender | Male / Female | Male |
| CardType | Type of HDFC Card | Millennia, Regalia, Diners Black, Infinia, Gold |
| City | Transaction City | Delhi, Mumbai, Pune, Bengaluru, Chennai, Hyderabad, Kolkata, Ahmedabad |
| TransactionCategory | Category | Groceries, Fuel, Bills, Travel, Shopping, Entertainment, Food |
| Merchant | Merchant Name | Swiggy, IRCTC, Amazon, HP Fuel etc. |
| PaymentStatus | Status | Paid, Due, Overdue |
| PaymentMode | Mode | UPI, Credit Card, Net Banking |
| IsFraudFlag | 0 = No, 1 = Fraud | 1 |
| AgeGroup | Customer Age Bucket | 18-25, 26-35, 36-45, 46-55, 56+ |
| CardLimit | Credit Limit | 100000 - 1000000 |
| TotalSpend | Spend Amount | 12000 |
| TotalDue | Due Amount | 5000 |
| RewardPoints | Reward Points | 120 |
| Fees | Late Fees | 500 |
| TransactionDate | Date | 2024-02-15 |

---

## 📊 Dashboard Pages Deep Dive - From Video

### PAGE 1: EXECUTIVE OVERVIEW

This is the landing page for CXOs. Clean HDFC blue theme with illustration of a man holding a card.

**KPI Cards (Top Row):**
- Total Spend - SUM(TotalSpend)
- Total Transactions - COUNT(TransactionID)
- Avg Ticket Size - AVERAGE(TotalSpend)
- Overdue Amount - SUM(TotalDue) where PaymentStatus = Overdue/Due
- Collection Efficiency - % of Paid vs Total

**Charts:**
1.  **Total Spend by MonthName** - Area Chart with smooth curve. Shows monthly seasonality. Jan, Feb, Mar, Apr 2024, 2025 months. Tooltip shows exact spend for month.
2.  **Total Spend and Sum of TotalDue by Year, Quarter, Month and Day** - Area chart with Year > Quarter > Month > Day hierarchy. Shows Total Spend vs Total Due trend. Can drill down.
3.  **Total Spend by TransactionCategory** - Horizontal Bar Chart. Categories sorted descending. Groceries is top in video.
4.  **Total Transactions by PaymentStatus** - Donut Chart with 500 total center. Segments: Paid (Blue), Due (Light Blue), Overdue (Darker).

**Interactivity shown in video:** Filter pane on right with Gender, CardType, City, Year. All KPI cards and charts are connected. Selecting CardType changes everything.

---

### PAGE 2: CUSTOMER & CARD ANALYTICS

Focuses on WHO is spending.

**Top Navigation Icons:** Document, Card, Chart, Wallet - shows this is Customer section.

**KPI Cards:** Total Reward Points (14M), Utilization % (15.27), Total Fees (54.80K) - These change based on gender filter as seen in video.

**Charts:**
1.  **Spend by Gender** - Pie Chart - Male vs Female. In video, Male is ~52.72% and when filtered to Male only, it becomes 100% donut.
2.  **Total Spend by CardType** - Treemap. Visual hierarchy: Millennia block is largest, then Diners Black, Regalia, etc. In video hover shows CardType Infinia Total Spend 6345.
3.  **Total Transactions by PaymentMode and TransactionCategory** - 100% Stacked Bar Chart. Shows for each category (Shopping, Bills, Fuel, Travel, Groceries, Food, Entertainment) what % is UPI vs Credit Card vs Net Banking.
4.  **Total Spend by City and AgeGroup** - Clustered Column Chart. X-axis = City, Legends = AgeGroup, Y-axis = Total Spend. Shows Bengaluru, Delhi, Mumbai etc. each with age group bars.

**Left Slicers in video:** TransactionCategory (with search), Merchant (with search), Gender (Male/Female). When user selects one, Treemap and Column chart filter.

**Bottom Illustration:** Two HDFC credit cards (XXXX XXXX 1234) and a man with bar chart - branding.

---

### PAGE 3: TRANSACTIONS & RISK DETAIL

Most important for Risk Team.

**Top Filters (Video):** IsFraudFlag, CardLimit (range slider), AgeGroup, PaymentStatus

**KPI Cards:**
- Fraud Count - 111 (COUNT where IsFraudFlag=1)
- Total Fees - 54.80K
- Utilization % - 15.27
- Overdue Amount - 2M

**Charts:**
1.  **Total Spend by Year and TransactionCategory** - Ribbon Chart - BEST visual. Shows how category rank changes from 2024 to 2025. Video tooltip: "2024 Groceries Total Spend 88334, 2025 Groceries Total Spend 71085, Total Spend Change -17249 (-22.98%), 2024 Groceries Rank 1, 2025 Rank 3, Rank Change -2". Ribbon flows show transition.

2.  **Fraud Count by City** - Funnel Chart - Shows fraud concentration. In video: Pune 20 (100%), Bengaluru 18 (90%), Delhi 5 (25%), etc. Funnel narrows as fraud count decreases. Very effective for risk.

3.  **Overdue Amount by City and TransactionCategory** - Treemap - Large blocks = high overdue. Video tooltip: "City Ahmedabad TransactionCategory Fuel Overdue Amount 54730", "City Chennai TransactionCategory Fuel", "City Hyderabad Fuel" etc. Shows which city+category combo is risky.

**Interactivity shown:** At 0:50, filtering IsFraudFlag from All to 1 keeps 111. At 0:52, CardLimit slider filtered to lower limit makes Overdue Amount 561K and Total Fees 10.58K. At 1:00, AgeGroup 46-55 selected -> Fraud Count 21, Overdue 97K. At 1:03, AgeGroup 56+ -> Fraud 9, Overdue 50K. At 1:08, PaymentStatus = Overdue -> Fraud 4, at 1:11 PaymentStatus = Due -> Fraud 2. This shows dynamic risk filtering.

---

## 🎨 Design & UI - GitHub Template

**Background Template:** I have a custom background template hosted on GitHub in `/assets/hdfc_background.png` and `/assets/hdfc_background_2.png`.

The template includes:
- Light blue gradient background (#E6F0FF to #FFFFFF)
- White rounded card containers with shadow
- HDFC Bank Logo top-left (Red & Blue)
- Icons: Document, Card, Chart, Wallet in blue squares
- Illustrations: Man with laptop, Woman with card, Woman holding credit card
- Footer navigation: Home_page, Executive_Overview, Customer_card_&_Analytics, Transactions_And_Risk_Detail

**How I used it in Power BI:**
- Power BI > View > Customize Current Theme > Import JSON from GitHub
- Insert > Image > Background from `/assets`
- Send to Back, set transparency 0%
- All visuals set to transparent background with white card effect.

This gives a premium banking dashboard look vs default Power BI.

---

## 🧮 DAX Measures Used

```dax
Total Spend = SUM('HDFC_Data'[TotalSpend])

Total Transactions = COUNT('HDFC_Data'[TransactionID])

Avg Ticket Size = DIVIDE([Total Spend], [Total Transactions], 0)

Overdue Amount = CALCULATE(SUM('HDFC_Data'[TotalDue]), 'HDFC_Data'[PaymentStatus] IN {"Due", "Overdue"})

Collection Efficiency = DIVIDE( CALCULATE(COUNT('HDFC_Data'[TransactionID]), 'HDFC_Data'[PaymentStatus]="Paid"), [Total Transactions]) * 100

Fraud Count = CALCULATE(COUNT('HDFC_Data'[TransactionID]), 'HDFC_Data'[IsFraudFlag]=1)

Total Fees = SUM('HDFC_Data'[Fees])

Utilization % = AVERAGE('HDFC_Data'[Utilization])

Total Reward Points = SUM('HDFC_Data'[RewardPoints])
```

---

## 💡 Key Insights From Video

Insights you can mention on LinkedIn:

1.  **Executive:** Spend is seasonal, dips in certain months, Collection Efficiency is around 30% and changes with city filter.
2.  **Customer:** Male customers spend slightly more, Millennia card is the most used card by spend, Bengaluru and Delhi are top cities, 36-45 age group is highest spender.
3.  **Risk:** Total 111 frauds detected, Bengaluru and Pune are fraud hotspots, Fuel and Travel categories have highest overdue amount, Hyderabad Fuel overdue is high, Fraud reduces drastically when CardLimit is low and AgeGroup is higher, Due/Overdue payment status isolates risky customers.

---

## 🛠️ Tools & Technologies

- **Power BI Desktop (Latest)**
- **Power Query** - For cleaning, removing duplicates, changing types
- **DAX** - For all KPIs
- **GitHub** - For hosting background template and version control
- **Figma / PowerPoint** - For background template design

---

## 📁 Project Structure

```
HDFC-Bank-Credit-Card-Dashboard/
│
├── assets/
│   ├── hdfc_background.png (GitHub Template)
│   ├── hdfc_background_2.png
│   └── icons/
│
├── screenshots/
│   ├── Executive_Overview.png
│   ├── Customer_Analytics.png
│   └── Risk_Detail.png
│
├── video/
│   └── video_HDFC_working.mp4 (Interactive Walkthrough)
│
├── data/
│   └── HDFC_Credit_Card_Dataset.csv
│
├── HDFC_Bank_Dashboard.pbix (Main Power BI File)
├── README.md (This File)
└── LICENSE
```

---

## 🚀 How to Run This Project

1.  Clone the repo:
    ```bash
    git clone https://github.com/your-username/HDFC-Bank-Credit-Card-Dashboard.git
    ```
2.  Open `HDFC_Bank_Dashboard.pbix` in Power BI Desktop
3.  If background not loading, manually add from `assets/` folder: Insert > Image > Select background.png > Send to Back
4.  Go to Transform Data to see Power Query steps
5.  Press Ctrl + Click on visuals to see interactions
6.  Play the video in `/video` folder to understand filtering logic

---

## 📸 Screenshots

> Add screenshots here after exporting from Power BI.

- Executive Overview
- Customer & Card Analytics  
- Transactions & Risk Detail

---

## 🔮 Future Improvements

- Add What-If parameter for Credit Limit simulation
- Add Anomaly Detection for fraud prediction using Python visual
- Connect to live SQL database instead of CSV
- Add Mobile Layout view
- Add Row Level Security (RLS) for City-wise managers

---

## 👨‍💻 Author & Connect

**Your Name** - Aspiring Data Analyst | Power BI Developer | Banking Analytics Enthusiast

- LinkedIn: [linkedin.com/in/your-profile]
- GitHub: [github.com/your-username]
- Portfolio: [your-portfolio-link]

If you liked this project, please give a ⭐ Star to this repo!

---

### Hashtags for GitHub Topics
`power-bi` `hdfc-bank` `credit-card-analytics` `banking-dashboard` `data-analytics` `fraud-detection` `business-intelligence` `dax` `data-visualization` `risk-analytics`


