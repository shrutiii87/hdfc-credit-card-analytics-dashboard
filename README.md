# HDFC Bank Credit Card Analytics Dashboard 💳📊

<img width="1200" height="420" alt="Hdfc-Credit-Card-Analytics-Animated" src="https://github.com/user-attachments/assets/99a97460-04e4-4fc9-9b54-4adcd90b36e1" />

## 📌 Overview

This repository contains a complete **HDFC Bank Credit Card Analytics Dashboard** built in **Microsoft Power BI**. 

This is not a static dashboard. As you can see in the attached video `video_HDFC_working.mp4`, the entire dashboard is **fully interactive** - every KPI card, chart, and visual responds instantly to slicers. The project demonstrates end-to-end BI workflow: Data Cleaning -> Data Modeling -> DAX -> UI Design -> Interactive Visualizations.

The dashboard uses a **custom HDFC-themed background template** hosted on GitHub (`/assets` folder) to give it a professional banking look - light blue gradient, clean cards, HDFC logo, and illustrated characters.

This project is ideal for showcasing skills for **Data Analyst, Business Analyst, and Power BI Developer** roles in Banking and Finance domain.

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

## 📊 Dashboard Pages Deep Dive 

### Home page 

<img width="960" height="540" alt="Home page" src="https://github.com/user-attachments/assets/7d7b8ef7-a59c-4759-b7af-16569e93d68e" />


---

### PAGE 1: EXECUTIVE OVERVIEW

<img width="1189" height="670" alt="image" src="https://github.com/user-attachments/assets/411c0b92-54c4-43bc-b533-e005398ebd6e" />

---

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

---

### PAGE 2: CUSTOMER & CARD ANALYTICS

<img width="1163" height="661" alt="image" src="https://github.com/user-attachments/assets/838367c2-9e23-49b4-81f0-0e3b83a2dd9f" />


---

Focuses on WHO is spending.

**Top Navigation Icons:** Document, Card, Chart, Wallet - shows this is Customer section.

**KPI Cards:** Total Reward Points (14M), Utilization % (15.27), Total Fees (54.80K) - These change based on gender filter as seen in video.

**Charts:**
1.  **Spend by Gender** - Pie Chart - Male vs Female. In video, Male is ~52.72% and when filtered to Male only, it becomes 100% donut.
2.  **Total Spend by CardType** - Treemap. Visual hierarchy: Millennia block is largest, then Diners Black, Regalia, etc. In video hover shows CardType Infinia Total Spend 6345.
3.  **Total Transactions by PaymentMode and TransactionCategory** - 100% Stacked Bar Chart. Shows for each category (Shopping, Bills, Fuel, Travel, Groceries, Food, Entertainment) what % is UPI vs Credit Card vs Net Banking.
4.  **Total Spend by City and AgeGroup** - Clustered Column Chart. X-axis = City, Legends = AgeGroup, Y-axis = Total Spend. Shows Bengaluru, Delhi, Mumbai etc. each with age group bars.


---

### PAGE 3: TRANSACTIONS & RISK DETAIL

<img width="1177" height="673" alt="image" src="https://github.com/user-attachments/assets/d2421f54-c318-4582-af3d-258184cfa452" />

---

Most important for Risk Team.

**Top Filters:** IsFraudFlag, CardLimit (range slider), AgeGroup, PaymentStatus

**KPI Cards:**
- Fraud Count - 111 (COUNT where IsFraudFlag=1)
- Total Fees - 54.80K
- Utilization % - 15.27
- Overdue Amount - 2M

**Charts:**
1.  **Total Spend by Year and TransactionCategory** - Ribbon Chart - BEST visual. Shows how category rank changes from 2024 to 2025. Video tooltip: "2024 Groceries Total Spend 88334, 2025 Groceries Total Spend 71085, Total Spend Change -17249 (-22.98%), 2024 Groceries Rank 1, 2025 Rank 3, Rank Change -2". Ribbon flows show transition.

2.  **Fraud Count by City** - Funnel Chart - Shows fraud concentration. In video: Pune 20 (100%), Bengaluru 18 (90%), Delhi 5 (25%), etc. Funnel narrows as fraud count decreases. Very effective for risk.

3.  **Overdue Amount by City and TransactionCategory** - Treemap - Large blocks = high overdue. Video tooltip: "City Ahmedabad TransactionCategory Fuel Overdue Amount 54730", "City Chennai TransactionCategory Fuel", "City Hyderabad Fuel" etc. Shows which city+category combo is risky.

---

## 🎨 Design & UI - GitHub Template

**Background Template:** I have a custom background template hosted on GitHub in asset folder

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

## 💡 Key Insights 

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

## 🚀 How to Run This Project

1.  Clone the repo:
    ```bash
    git clone https://github.com/your-username/HDFC-Bank-Credit-Card-Dashboard.git
    ```
2.  Open `HDFC_Bank_Dashboard.pbix` in Power BI Desktop
3.  If background not loading, manually add from `assets/` folder: Insert > Image > Select background.png > Send to Back
4.  Go to Transform Data to see Power Query steps
5.  Press Ctrl + Click on visuals to see interactionsc

---

## 🔮 Future Improvements

- Add What-If parameter for Credit Limit simulation
- Add Anomaly Detection for fraud prediction using Python visual
- Connect to live SQL database instead of CSV
- Add Mobile Layout view
- Add Row Level Security (RLS) for City-wise managers
