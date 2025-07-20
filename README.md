# 📦 AI-Driven Supply Chain Analysis with Quadratic, n8n, and Supabase

![Banner](https://github.com/SachinSavkare/AI-Driven-Supply-Chain-Analysis-N8N-Quadratic-Supabase/blob/main/AI-Driven%20Supply%20Chain%20Workflow.png) <!-- Replace with your custom banner -->

## 📚 Table of Contents
- [🚀 Project Overview]
- [📂 Project Structure & Tools Used]
- [🛠️ Automation Workflow (n8n)]
- [🧽 Data Cleaning & Summary Table]
- [📊 Calculated KPIs (SCOR-aligned)]
- [📈 Insights and Business Questions]
- [🧠 Visual Analysis for Stakeholders]
- [📋 Final Recommendations]
- [🧮 Formulas Used]
- [📷 Slide Gallery]
- [📌 How AI Enhanced the Workflow]
- [🧾 Conclusion]
- [📎 License & Credits]

---

## 🚀 Project Overview

This project demonstrates how we used AI tools like **Quadratic** and **n8n** to automate and analyze complex supply chain operations for a fictional FMCG company – **Atlique Mart**.  
By integrating email-based data ingestion, PostgreSQL (via Supabase), and an AI-powered spreadsheet interface, we performed **deep analytics** on fulfillment, order cycle, delivery reliability, and demand patterns.

> 🎯 **Objective**: Automate data processing and generate SCOR-based performance KPIs using modern AI tools for smarter decision-making.

---

## 📂 Project Structure & Tools Used

| Layer               | Tool/Platform         | Purpose                             |
|--------------------|------------------------|-------------------------------------|
| Automation Layer    | n8n (Self-hosted)      | Email monitoring & CSV ingestion    |
| Data Storage        | PostgreSQL (Supabase)  | Cloud-native DB for scale           |
| Analytics Layer     | Quadratic              | AI spreadsheet for report creation  |
| Visualization Layer | PowerPoint             | Dashboard presentation              |

---

## 🛠️ Automation Workflow (n8n)

![Step 1 - n8n Workflow](https://github.com/SachinSavkare/AI-Driven-Supply-Chain-Analysis-N8N-Quadratic-Supabase/blob/main/Workflow.png)

- Watch Gmail for 3PL shipment emails (India & USA)
- Extract attached CSVs (e.g., `fact_order_line_India_*.csv`)
- Convert CSV → JSON → Cleaned → Uploaded to Supabase
- Data appended daily after verifying date cutoff (e.g., `2025-05-16`)

---

## 🧽 Data Cleaning & Summary Table

![Step 2 - Data Cleaning](https://github.com/SachinSavkare/AI-Driven-Supply-Chain-Analysis-N8N-Quadratic-Supabase/blob/main/Data%20Cleaning.png)

- Loaded all dimension & fact tables:
  - `dim_customer`, `dim_product`, `dim_target_orders`
  - `fact_order_line`, `fact_aggregate`, `dim_date`, `exchange_rate`
- Cleaned: nulls, data types, whitespaces
- Generated new consolidated table: `fact_summary`

---

## 📊 Calculated KPIs (SCOR-aligned)

![Step 3 - KPIs](https://github.com/SachinSavkare/AI-Driven-Supply-Chain-Analysis-N8N-Quadratic-Supabase/blob/main/Domain.png)

The following KPIs were calculated in the fact_summary table:

- ✅ **OTIF %** (On Time In Full)
- 🕒 **Order Cycle Time** (in days)
- ⏱ **Average Delivery Delay**
- 📦 **Backorder Quantity**
- 📈 **Lead Time Variability**
- 📉 **Category Demand Variability**
- 🧮 **Total Order Lines**, **Total Orders**, **Fill Rate %, etc.**

> See [Formulas Used](#-formulas-used) below.

## 🧾 Business Question Prompts

To view all the natural language prompts used in **Quadratic AI** for solving key supply chain business questions, refer to the document below:

📄 [View Prompt Document](https://github.com/SachinSavkare/AI-Driven-Supply-Chain-Analysis-N8N-Quadratic-Supabase/blob/main/Prompt%20for%20New%20Tables%20%2C%20Columns%2C%20Business%20Ex%201%20%2C2%203.docx.pdf)


## 📈 Insights and Business Questions (Quadratic)

![Step 4 - Business Questions]

AI-generated answers to business questions using natural language prompts in Quadratic:

### ✅ Exercise 1:
1. Show me Monthly On time Performnace by Cities  
2. Show me top 5 customers based on order value and their OTIF %, IF %, OT %.  
3. Show me top 5 customers in India based on order value and their OTIF %, IF %, OT %.  
4. Quantify the revenue loss attributed to undelivered orders  
5. Identify customers with the most significant OTIF discrepancies  
6. Determine product categories that exhibit low 'In Full' delivery rates  
7. Calculate the average delay time for late deliveries  
8. Identify product categories with the lowest 'In Full' delivery rates  

### 📊 Exercise 2:
1. Which product categories are facing the highest fulfillment and delivery challenges?  
2. Are any customers consistently missing OTIF targets?  
3. Where is lead‑time variability threatening service levels?  
4. Which weeks experienced the worst demand swings and did that impact service?  
5. Do long delivery delays correlate with larger backorders?  
6. Which customers are improving—or worsening—in order cycle time?  
7. Are metro and non‑metro customers served differently?  

---

## 🧠 Visual Analysis for Stakeholders

![Step 5 - Visual Insights](https://github.com/SachinSavkare/AI-Driven-Supply-Chain-Analysis-N8N-Quadratic-Supabase/blob/main/Business%20Question%20Solution.pdf)

- Weekly & monthly performance graphs
- Customer-wise OTIF trends
- Category-wise fulfillment summaries
- Flags: Red (<60%), Yellow (60–80%), Green (>80%)

---

## 📋 Final Recommendations

![Step 6 - Recommendations](https://github.com/SachinSavkare/AI-Driven-Supply-Chain-Analysis-N8N-Quadratic-Supabase/blob/main/%F0%9F%93%A6%20Supply%20Chain%20Performance%20Report.docx.pdf)

- Stabilize fulfillment for **Beverages & Dairy**
- Track **lead time variability** weekly
- Improve OTIF via **city-specific distribution tweaks**
- Introduce **weekly alerts for demand surges**

---

## 🧮 Formulas Used

| Column / KPI                 | Formula                                                             |
|-----------------------------|----------------------------------------------------------------------|
| `backorder_qty`             | `order_qty - delivery_qty`                                          |
| `order_cycle_time_days`     | `actual_delivery_date - order_placement_date`                       |
| `delivery_delay_days`       | `actual_delivery_date - agreed_delivery_date`                       |
| `in_full_percent`           | `(delivery_qty / order_qty) * 100`                                  |
| `on_time_flag`              | `1 if actual_delivery_date <= agreed_delivery_date else 0`          |
| `lead_time_variability`     | `Std Dev of order_cycle_time_days by category`                      |
| `category_demand_variability` | `Std Dev of weekly order_qty by product category`               |
| `OTIF %`                    | `% of orders where on_time_flag = 1 and in_full_percent = 100`      |

---

## 📷 Slide Gallery

You can explore the full slide deck used in this analysis by downloading the presentation file below:

🎞️ [Download Presentation1.pptx](https://github.com/SachinSavkare/AI-Driven-Supply-Chain-Analysis-N8N-Quadratic-Supabase/blob/main/Presentation1.pptx)

> The slides cover step-by-step visuals for automation setup, data cleaning, KPI reports, and business insights for stakeholders.

---

## 📌 How AI Enhanced the Workflow

- ⛳ **n8n** automated tedious email ingestion & transformation  
- 📉 **Quadratic** enabled spreadsheet-like AI analysis via prompts  
- 💡 **SCOR KPIs** were generated automatically without writing SQL  
- 📊 Visuals auto-generated for stakeholder use

---

## 🧾 Conclusion

This project shows how **AI and automation** can drastically improve supply chain analytics:

- ✅ Zero manual effort from CSV to analysis
- ✅ Real-time dashboards powered by AI prompts
- ✅ Actionable supply chain insights in hours, not weeks
- ✅ Stakeholders gain better visibility and faster decisions

---

## 📎 License & Credits

- Tools Used: [n8n](https://n8n.io) | [Supabase](https://supabase.com) | [Quadratic](https://quadratic.to) | [PostgreSQL](https://www.postgresql.org/)  
- Developed by: **[Your Name]**  
- © 2025 Supply Chain Analytics Portfolio Project
