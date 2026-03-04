# 📊 Marketing Campaign Performance Analysis | Multi-Channel Digital Advertising Insights | Power BI

> **Business Question:** How can we optimize marketing budget allocation across channels, cities, and campaigns to maximize ROI and conversion efficiency?
>
> **Domain:** Digital Marketing / Multi-Channel Advertising
>
> **Tools Used:** Power BI Desktop · DAX · Excel

**Author:** Phan Trung Hiếu
**Date:** 2023–2024
**Tools Used:** Power BI · DAX · Microsoft Excel

---

## 📑 Table of Contents

1. [📌 Background & Overview](#-background--overview)
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)
3. [🧠 Design Thinking Process](#-design-thinking-process)
4. [📊 Key Insights & Visualizations](#-key-insights--visualizations)
5. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)

---

## 📌 Background & Overview

### Objective

### 📖 What is this project about?

This project analyzes the performance of a 2023 multi-channel digital marketing campaign across Facebook, Instagram, and Pinterest — covering three UK cities (Birmingham, London, Manchester) and three seasonal campaigns (Spring, Summer, Fall).

The objective is to turn fragmented, channel-specific ad data into a unified, actionable Power BI dashboard that enables data-driven decision-making.

✔️ Measure and compare marketing ROI, CPA, CTR, CVR, and Engagement Rate across channels, devices, campaigns, and geographies.

✔️ Identify the highest-performing channel–city combinations to guide future budget allocation.

✔️ Uncover seasonal performance trends to optimize campaign timing and creative strategy.

✔️ Provide an interactive, executive-ready dashboard that replaces manual Excel reporting.

### 👤 Who is this project for?

✔️ Marketing Managers & Heads of Marketing who need a single source of truth for campaign performance.

✔️ Data Analysts & BI Developers looking for a reference Power BI project with star-schema modeling and advanced DAX.

✔️ Decision-makers & Stakeholders who need to justify and optimize ad spend across platforms.

---

## 📂 Dataset Description & Data Structure

### 📌 Data Source

- **Source:** Simulated digital advertising dataset (internal/educational)
- **Size:** 9,900 rows × 18 columns (1 fact table + 4 dimension tables after modeling)
- **Format:** `.xlsx` (Excel)
- **Period:** March – November 2023

### 📊 Data Structure & Relationships

#### 1️⃣ Tables Used

The raw data was modeled into a **Star Schema** with 1 fact table and 4 dimension tables:

| Table | Type | Description |
|---|---|---|
| `factMKT` | Fact | Daily ad performance metrics (clicks, spend, conversions, etc.) |
| `dimDate` | Dimension | Date hierarchy (Day, Month, Month Number, Month Short) |
| `dimChannel` | Dimension | Channel (Facebook, Instagram, Pinterest) and Device |
| `dimCampaign` | Dimension | Campaign name (Spring, Summer, Fall) |
| `dimLocation` | Dimension | City/Location with Latitude & Longitude |
| `dimAd` | Dimension | Ad type (Collection, Discount) |

#### 2️⃣ Table Schema & Data Snapshot

**Table: factMKT (Fact Table)**

| Column Name | Data Type | Description |
|---|---|---|
| Date | DATE | Date of daily ad performance record |
| Clicks | FLOAT | Daily clicks for each ad |
| Impressions | FLOAT | Daily times ad was shown to viewers |
| CTR, % | FLOAT | Daily average click-through rate |
| Daily Average CPC | FLOAT | Daily average cost-per-click (GBP) |
| Spend, GBP | FLOAT | Total daily advertising spend (GBP) |
| Conversions | INT | Total daily purchases attributed to ad |
| Total conversion value, GBP | FLOAT | Revenue from conversions (GBP) |
| Comments | FLOAT | Total daily comments per ad |
| Likes (Reactions) | FLOAT | Total daily likes/reactions per ad |
| Shares | FLOAT | Total daily shares per ad |
| dimAd.Ad Key | FK | Foreign key → dimAd |
| dimCampaign.Campaign Key | FK | Foreign key → dimCampaign |
| dimChannel.Channel Key | FK | Foreign key → dimChannel |

<details>
<summary>📋 Click to see Dimension Tables</summary>

**dimDate**

| Column Name | Data Type | Description |
|---|---|---|
| Date | DATE | Primary key |
| Day | INT | Day of month |
| Day of Week | TEXT | Day name |
| Month | TEXT | Full month name |
| Month Number | INT | Month number (1–12) |
| Month Short | TEXT | Abbreviated month (Mar, Apr…) |

**dimChannel**

| Column Name | Data Type | Description |
|---|---|---|
| Channel Key | INT | Primary key |
| Channel | TEXT | Facebook / Instagram / Pinterest |
| Device | TEXT | Desktop / Mobile / Tablet |

**dimCampaign**

| Column Name | Data Type | Description |
|---|---|---|
| Campaign Key | INT | Primary key |
| Campaign | TEXT | Spring / Summer / Fall |

**dimLocation**

| Column Name | Data Type | Description |
|---|---|---|
| Location Key | INT | Primary key |
| City/Location | TEXT | Birmingham / London / Manchester |
| Latitude | FLOAT | Geographic latitude |
| Longitude | FLOAT | Geographic longitude |

**dimAd**

| Column Name | Data Type | Description |
|---|---|---|
| Ad Key | INT | Primary key |
| Ad | TEXT | Collection / Discount |

</details>

#### 3️⃣ Data Relationships

The model follows a **Star Schema** design — `factMKT` sits at the center with one-to-many relationships connecting to all five dimension tables via surrogate keys.

> 📸 *Data Model Screenshot:*

<img width="898" height="625" alt="Screenshot 2026-03-04 112247" src="https://github.com/user-attachments/assets/4bf106af-8322-4eac-adc9-1e36b7ae3d0a" />


---

## 🧠 Design Thinking Process

This project followed the 5-stage Design Thinking framework to ensure the dashboard genuinely serves stakeholder needs — not just displays data.

### 1️⃣ Empathize — Nhìn rộng (See the big picture)

**Primary Stakeholder:** Marketing Manager / Head of Marketing

**5W1H Analysis:**

| Question | Answer |
|---|---|
| **Who** views this dashboard? | Marketing Manager, Head of Marketing |
| **What** problem does it solve? | Tracking, measuring & analyzing multi-channel campaign performance to find optimization insights |
| **When & Where** is it used? | Daily check-ins, weekly review meetings, monthly/quarterly planning — on desktop, in meeting rooms, or on tablet |
| **Why** is this needed? | Shift from gut-feel to data-driven decisions; maximize ROI per ad dollar; identify which channels & regions perform best |
| **How** do stakeholders decide? | Compare KPIs (ROI, CPA, Conversions) across channels (Facebook vs Instagram), regions (Birmingham vs London), and campaigns (Spring vs Fall) |

**Stakeholder Pain Points:**
- Wasting hours manually consolidating data from Facebook Ads Manager and Google Analytics
- Difficulty making fair "apples-to-apples" comparisons across channels
- Hard to spot trends and hidden insights behind raw numbers
- Pressure to prove ROI to senior leadership

**Stakeholder Gains:**
- One single source of truth for all marketing performance
- Quickly identify "stars" vs "drains" in the marketing mix
- Confidently make data-backed budget allocation decisions
- Present results visually and professionally to executives

### 2️⃣ Define Point of View — Nhìn sâu (Go deeper)

**Northstar Metrics:**

| Metric | Formula | Why This Metric? |
|---|---|---|
| **Marketing ROI** | `(Total Conversion Value - Spend) / Spend` | The ultimate measure of profitability — directly links marketing to financial outcomes |
| **Cost Per Acquisition (CPA)** | `Spend / Conversions` | Measures cost efficiency at the micro level — enables fair channel-by-channel comparison |

**Key Points of View (Analytical Angles):**

| POV | Description | Business Value |
|---|---|---|
| **Overall Performance** | 360° health check of all campaigns | Answer "Are we doing well overall?" |
| **Channel & Device Performance** | Compare Facebook, Instagram, Pinterest across devices | Decide which platform deserves more budget |
| **Geographic Performance** | Map-level analysis across Birmingham, London, Manchester | Identify high-potential markets and regional strategy |
| **Ad Creative Performance** | Compare Collection vs Discount ad types | Understand which content resonates most with customers |

**Key Business Questions:**
1. What is the overall performance of all marketing campaigns (total cost, revenue, ROI)?
2. Which channel (Facebook, Instagram, Pinterest) and device deliver the highest ROI?
3. Which city has the best conversion rate and lowest CPA?
4. Which ad type (Collection, Discount) performs best for engagement and conversions?
5. How does performance change over time (weekly/monthly)?

### 3️⃣ Ideate — Ý tưởng (Generate ideas)

**Dashboard Structure (4 Pages):**

| Page | Role | Key Visuals |
|---|---|---|
| **Overview** | Executive summary — answer the "big picture" questions | KPI scorecards, trend line chart, impressions/clicks/conversions bar, spend by channel, KPI waterfall |
| **Channel** | Deep-dive into channel & device performance | Clicks & CPC by month and channel, bubble chart (CPC vs CTR), ROAS/profit breakdown, Sankey flow |
| **City** | Geographic analysis | Impressions/engagement by channel, likes/shares/comments breakdown, ROAS scatter, profit bar + line |
| **Ad & Campaign** | Campaign and creative performance | Spend & profit by campaign, sales by campaign + ad, conversion rate funnel, KPI comparison table |

**Metric Hierarchy:**
- **Layer 0 (Scorecards):** Total Sales, Total Profit, Total Spend, Conversion %, Engagement %, ROI
- **Layer 1 (Trend):** Metrics over time (monthly)
- **Layer 2 (Cross-dimension):** Metrics broken down by Channel × Device, City × Channel, Campaign × Ad

### 4️⃣ Prototype & Review

The dashboard was iterated through multiple drafts, evaluating each page on:
- **Information quality** — Is the right data shown?
- **Chart effectiveness** — Does the chart type match the question?
- **Layout** — Is the hierarchy clear?
- **Color** — Does the dark green theme aid readability?
- **Labels** — Are axes, units, and titles clearly labeled?

---

## 📊 Key Insights & Visualizations

### 🔍 Dashboard Preview

#### 1️⃣ Overview Dashboard

<img width="1788" height="778" alt="Screenshot 2026-03-04 112207" src="https://github.com/user-attachments/assets/8c445de6-c75e-406d-82d8-915b3a99de37" />

📌 **Analysis:**

- **Observation:** Total Sales reached **£1.73M** with a Total Profit of **£1.57M** and Total Spend of only **£0.16M**, yielding an impressive **ROI of 960.77%**. Sales peaked in **September** (£259K), correlating with the Fall campaign launch. Conversion rate stands at **22.17%** while Engagement Rate is **5.46%**. Facebook leads spend at **£72K**, followed by Instagram (£63K) and Pinterest (£28K). All three KPIs (Sales, Profit, Spend) show a positive trend vs. prior month.

- **Recommendation:** The Fall campaign in September is a clear high-performer — consider front-loading budget into this period in future cycles. Pinterest's low spend-to-result ratio warrants investigation: it may be under-invested relative to its potential.

---

#### 2️⃣ Channel Dashboard

<img width="1304" height="730" alt="Screenshot 2026-03-04 112214" src="https://github.com/user-attachments/assets/479923d0-731a-4d55-bd69-0817e5c21eb4" />

📌 **Analysis:**

- **Observation:** Pinterest achieves the **lowest CPC (£0.66)** and **highest CVR (26.81%)** and **ROAS (~£20)**, making it the most cost-efficient channel despite receiving the smallest budget. Instagram has the **highest CTR (1.42%)** and a strong CPA of **£4.07**. Facebook drives the most absolute clicks (7.4K–11.1K/month) but has the highest CPC (£1.02) and lowest CVR (18.77%). CPC peaks in August–September across all channels, suggesting seasonal ad auction competition increases.

- **Recommendation:** Reallocate a portion of Facebook's budget toward Pinterest, which demonstrates superior efficiency metrics. Run A/B tests on Facebook to improve CVR before scaling spend further.

---

#### 3️⃣ City Dashboard

<img width="1295" height="729" alt="Screenshot 2026-03-04 112219" src="https://github.com/user-attachments/assets/72d72955-8300-4715-a44d-813e4c2dc1aa" />

📌 **Analysis:**

- **Observation:** Facebook dominates **impressions (5.4M)** followed by Instagram (4.8M) and Pinterest (4.4M). Engagement rates are highest on Pinterest (5.8%), driven by strong like ratios (~77%). Across all channels, **Likes account for 74–77%** of total engagements. Instagram generates the highest ROAS (~£20) with moderate spend (~£60K), while Facebook achieves higher absolute profit (£0.34M vs Instagram £0.62M vs Pinterest £0.61M).

- **Recommendation:** Instagram and Pinterest show a superior profit-to-spend ratio. Cities with lower engagement (e.g., Birmingham for certain channels) should receive targeted creative refreshes. Geo-specific campaigns should be explored for Manchester, which shows strong conversion potential.

---

#### 4️⃣ Ad & Campaign Dashboard

<img width="1295" height="727" alt="Screenshot 2026-03-04 112224" src="https://github.com/user-attachments/assets/82be3b4c-80a3-4d54-8452-fef1d086fa19" />

📌 **Analysis:**

- **Observation:** The **Fall campaign** dramatically outperforms Spring and Summer — generating **£0.67M profit** on just **£79K spend**, vs Spring's **£0.45M profit** on **£50K spend**. Summer is the weakest campaign (lowest profit and highest relative spend). **Discount ads** consistently outperform Collection ads in total sales across all campaigns. Conversion rate peaks in **Summer (32.85%)** but drops sharply in Fall (17.49%), suggesting Summer converts better per impression but drives fewer total sales. The KPI table confirms **Pinterest has the best CPA (£2.45)** and the highest CVR (26.81%).

- **Recommendation:** Prioritize the **Fall campaign** for budget concentration. Investigate the Summer conversion rate spike — if replicable, it could unlock a high-efficiency summer strategy. Scale Discount ad creatives across all channels, particularly on Pinterest and Instagram.

---

## 🔎 Final Conclusion & Recommendations

Based on the analysis, we recommend the **Marketing team** consider the following:

**💰 Budget Reallocation:**
- Shift 15–20% of Facebook budget to Pinterest, which delivers the best ROI efficiency (lowest CPC, highest CVR)
- Concentrate campaign budgets in the **Fall period (Sept–Nov)** where revenue and profit peaks are most pronounced

**📣 Channel Strategy:**
- Use **Instagram** as the primary awareness + conversion channel (balanced CTR, strong ROAS, high impressions)
- Use **Pinterest** as the efficiency channel (best CPA, CVR, ROAS per £ spent)
- Optimize **Facebook** creatives to improve its CVR before scaling spend

**🗺️ Geographic Focus:**
- Investigate **Manchester** for potential scale-up — early signals suggest competitive engagement metrics
- Tailor ad content by city based on channel-specific engagement patterns

**🎨 Creative Strategy:**
- Prioritize **Discount ads** over Collection ads — they consistently outperform in sales across all campaigns
- Invest in creative testing during the **Summer season** to capitalize on its unusually high conversion rate

**📈 Measurement:**
- Establish **ROI and CPA as primary KPIs** for all future campaign reviews
- Implement weekly performance check-ins using the Overview dashboard to catch spend inefficiencies early

---

*📁 Files included in this repository:*
- `Marketing_Campaign.pbix` — Power BI report file
- `DataSet.xlsx` — Raw data source
