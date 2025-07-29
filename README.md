# PowerBI_MakeOrBuy
# 📦 Power BI Supply Chain Optimization: A Make vs. Buy Case Study

## 🔍 Project Overview
This Power BI case study follows a simulated end-to-end supply chain analysis based on a real-world scenario provided by DataCamp. The purpose of this project is to support strategic sourcing and manufacturing decisions by modeling the cost implications of buying versus making critical product components.

Through dynamic parameterization, cost breakdown visualizations, and scenario planning tools, this project demonstrates a full-stack data analyst skillset, including data modeling, DAX development, visualization best practices, and business decision support.

---

## 🧭 Project Objectives
- Identify the lowest-cost supplier for each component at various production volumes.
- Calculate full cost (unit cost * volume + non-recurring costs) for each quote.
- Build a responsive dashboard to explore cost variation by volume and supplier.
- Incorporate internal manufacturing capacity and investment into "Make" calculations.
- Perform make-vs-buy analysis using dynamic scenario volumes.
- Adjust for quality-related yield rates per supplier.
- Present cost-avoidance and actionable recommendations.

---

## 🔨 Step-by-Step Journey

### 1. **Quote Exploration & Initial Setup**
I began with the `Quotes` table containing supplier offers for various `Part_Numbers`, `Volumes`, `Unit_Cost`, and `Non_Recurring_Expenses`.

- Changed summarization of `Volume` to *Don't Summarize*.
- Formatted `Unit_Cost` and `Non_Recurring_Expenses` as currency ($, 2 decimals).
- Created a column chart to show the number of quotes per part.
- Introduced a slicer for `Part_Number` and filtered visuals accordingly.
- Built a line chart showing how `Unit_Cost` changes with volume by supplier.
- Identified that **unit costs generally decreased as volumes increased**.

### 2. **Cost Modeling: Extended and Full Cost**
To move from unit-level insights to decision-making:
- Created `Extended Cost` = `Unit_Cost` * `Volume`
- Created `Full Cost` = `Extended Cost` + `Non_Recurring_Expenses`
- Built a visual table showing `Supplier`, `Part_Number`, `Volume`, and `Full Cost`

This helped answer:  
> _Which supplier offers the lowest full cost for P0622 at 5,000 units?_

### 3. **Visualizing Optimal Supplier Selection**
Created a dedicated **Supplier Selection** report page:
- Added slicers for `Part_Number` and `Volume` (single-selection).
- Added a Card visual to show the `Lowest Cost Supplier` dynamically.
- Built a stacked bar chart to visualize `Extended Cost` and `Non_Recurring_Expenses`.
- Used *Edit Interactions* to isolate visuals influenced by slicers.

### 4. **Scenario Analysis: Planning for Uncertain Demand**
Built a **Scenario Analysis** tool:
- Created a numeric parameter `Scenario Volume` (1,000 to 100,000 units).
- Built `Scenario Full Cost` measure using `MINX` over filtered `Quotes` where `Volume <= Scenario Volume`.
- Visualized `Scenario Volume` vs. `Full Cost` in a line chart.
- Added a vertical constant line marking the scenario volume.

Example question addressed:  
> _What is the full cost for P0604 at 75,000 units?_

### 5. **Role-Level Data Security for Stakeholders**
- Reviewed `Product_Dimension` table for `Project` column.
- Created roles: `Project Siliode` and `Project Kerfuffle` using DAX filters.
- Used **View As** to validate role-based data visibility.

### 6. **Incorporating Internal Manufacturing Costs (Make Option)**
- Analyzed `Internal_Mfg_Resource_Estimates`:
  - Fields: `Cost_per_Unit`, `Machine_Model`, `Unit_Capacity`, `Existing_Capacity`, `Machine_Fixed_Cost`
- Created:
  - `Additional Unit Capacity Required` = Scenario Volume - Existing Capacity (if > 0)
  - `Capital Investment Required (Make)` = `ROUNDUP(Additional Units / Unit_Capacity)` * `Machine_Fixed_Cost`
  - `Make Scenario - Full Cost` = (`Scenario Volume` * `Cost_per_Unit`) + `Capital Investment`
- Visualized total make cost and compared it against buy option.

Key question:  
> _How much capital investment is required to make 40,000 units of P1125?_

### 7. **Make vs. Buy Decision Engine**
- Created comparative table showing:
  - `Make Scenario Full Cost`
  - `Buy Scenario Full Cost`
  - `Make vs. Buy Decision`
  - `Cost Avoidance` = `ABS(Make - Buy)`
- Clustered column chart visualizing `Buy Full Cost` by supplier.

Answered:  
> _Do we Make or Buy P1227 at 21,000 units?_

### 8. **Factoring In Quality with Supplier Yield Rates**
- Created `Supplier Yield` table:
  - Widgetmakers: 72%, Ringo Nova: 83%, Others: 98%
- Related `Supplier Yield` to `Quotes`.
- Adjusted volume: `Adjusted Units Ordered = Scenario Volume / Yield Rate`
- Updated all full cost calculations using adjusted volume.

Answered:  
> _At 99,000 units, what cost should we expect to pay for \"Porlity\" given low supplier yield?_

---

## 📈 Key Features Implemented
- 📊 Advanced DAX Measures (`MINX`, `FILTER`, `ROUNDUP`, `IF`)
- 🔁 Dynamic Scenario Planning with Parameters
- 🧮 Cost Modeling: Unit, Extended, Full, Capital Investment
- 🔐 Row-Level Security by Project
- 🎯 Cost Avoidance and Recommendation Engine
- ⚙️ Data Normalization and Table Relationships
- 📉 Quality Adjustment via Yield Rate Logic

---

## 💼 Business Value & Impact
This project delivers a **comprehensive cost decision tool** that enables procurement teams and operations managers to:

- Make data-driven supplier choices with clear cost breakdowns.
- Dynamically analyze make-vs-buy decisions across demand volumes.
- Incorporate quality impacts into cost models, reducing hidden costs.
- Identify cost-avoidance opportunities and optimize total ownership cost.
- Avoid over-ordering or underutilizing internal capacity.

> _This dashboard could simulate millions of dollars in potential savings._

---

## 🔚 Conclusion
This Power BI case study showcases a high-impact analytical solution for complex supply chain scenarios. By combining data engineering, business acumen, and advanced Power BI techniques, this project simulates a powerful analytics product ready for real-world deployment.

> _\"Data analysis is not just about numbers—it's about making decisions that move the business forward.\"_

---


### 🧾 License: MIT
### [📥 Download the Power BI Report](Reports/MakeOrBuy.pbix)
