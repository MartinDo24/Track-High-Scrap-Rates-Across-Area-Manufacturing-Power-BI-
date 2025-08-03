# Production-process-analysis-PBI


Author: ĐỖ HOÀNG MINH  

Date: 2025-05-05  

Tools Used: Power BI  

## 📑 Table of Contents 

1.[📌 Background & Overview](#-background--overview)  

2.[📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  

3.[🧠 Design Thinking Process](#-design-thinking-process)

4.[📊 Key Insights & Visualizations](#-key-insights--visualizations)

5.[🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)
 

## 📌 Background & Overview 

### Objective

### 📖 What is this project about?  

✅Addresses scrap issues by identifying key locations and causes of waste

✅Reduces unsafe inventory risks through safety management and data analysis

✅Improves production efficiency by suggesting tools and processes to optimize quality

### 👤 Who is this project for?  

-Production director

-Strategic planners

-Data analysts

## 🎯 Project Outcome

1. Better visibility into key quality issues at the warehouse level
  
  + Track the Warehouse Rejection Rate with detailed breakdowns by product type, region, supplier, and rejection reason.

  + Enable stakeholders to detect patterns of poor quality and quickly identify high-risk areas or suppliers

2. Quantify and control product loss and failure costs

  - Measure the total quantity of defective products and associated financial losses across locations and time.

  - Identify which products or suppliers cause the highest costs, helping optimize sourcing and inspection strategies.

3. Support root cause analysis through multi-layered data views

   - Implement a Layer 0–2 dashboard structure:

      + Layer 0: High-level KPIs (e.g. defect rate, loss quantity, total cost)

      + Layer 1: Time-based breakdown (monthly/quarterly/yearly)

      + Layer 2: Combined views by region, product, time, and defect reason

   -This allows teams to drill down from overview to granular root causes efficiently.

4. Deliver actionable insights to guide supplier management and cost control

   - Provide clear answers to key stakeholder questions like:

   - Which products have the highest defect rate?

   - Which areas incur the most loss?

   - Which suppliers are underperforming?

   - These insights support strategic decisions on supplier evaluations, contract renegotiations, and internal quality policies.

5. Lay the foundation for an automated and scalable quality monitoring system

   - Ensure that quality data is automated, visualized, and updated regularly.

   - Allow easy extension to future metrics (e.g., inspection pass rate, delivery delays, returns from customers).

## 📂 Dataset Description & Data Structure  

### 📌 Data Source  

- Source: Used the data already in the PBIX file to make reports

- Size: 8 table ~ 100K rows

- Format: Production-process-analysis.pbix


### 📊 Data Structure & Relationships  

#### 1️⃣ Tables Used:

-Fact table:
  
  + F_Product_Product
  
  + F_Production_WorkOrderRouting

-Dim table:
  
  + D_Product_Inventory
  
  + D_Product_ProductTable
  
  + D_Production_Location
  
  + D_Production_ScapReason
  
  + D_Production_WorkOrder
  
  + DateTable

#### 2️⃣ Table Schema & Data Snapshot  

Table 1: F_Product_Product

| Column Name   | Data Type |
|---------------|-----------|
| ProductKey    | INT       |
| ProductName   | TEXT      |
| Category      | TEXT      |
| StandardCost  | FLOAT     |
| ListPrice     | FLOAT     |

Table 2: F_Production_WorkOrderRouting

| Column Name        | Data Type |
|--------------------|-----------|
| WorkOrderID        | INT       |
| OperationSequence  | INT       |
| LocationID         | INT       |
| ScheduledStartDate | DATE      |
| ScheduledEndDate   | DATE      |
| ActualStartDate    | DATE      |
| ActualEndDate      | DATE      |
| ActualResourceHrs  | FLOAT     |
| PlannedCost        | FLOAT     |
| ActualCost         | FLOAT     |

Table 3: D_Product_Inventory

| Column Name | Data Type |
|-------------|-----------|
| ProductID   | INT       |
| WarehouseID | INT       |
| Quantity    | INT       |
| LastUpdated | DATE      |

Table 4: D_Product_ProductTable

| Column Name        | Data Type |
|--------------------|-----------|
| ProductID          | INT       |
| ProductName        | TEXT      |
| ProductNumber      | TEXT      |
| Color              | TEXT      |
| SafetyStockLevel   | INT       |
| ReorderPoint       | INT       |

Table 5: D_Production_Location

| Column Name  | Data Type |
|--------------|-----------|
| LocationID   | INT       |
| LocationName | TEXT      |
| Availability | FLOAT     |
| CostRate     | FLOAT     |

Table 6: D_Production_ScapReason

| Column Name   | Data Type |
|----------------|----------|
| ScrapReasonID  | INT      |
| ReasonName     | TEXT     |

Table 7 : D_Production_WorkOrder

| Column Name  | Data Type |
|--------------|-----------|
| WorkOrderID  | INT       |
| ProductID    | INT       |
| OrderQty     | INT       |
| ScrappedQty  | INT       |
| StartDate    | DATE      |
| EndDate      | DATE      |
| DueDate      | DATE      |

Table 8: DateTable

| Column Name | Data Type |
|-------------|-----------|
| Date        | DATE      |
| Year        | INT       |
| Month       | INT       |
| MonthName   | TEXT      |
| Quarter     | INT       |
| WeekDay     | TEXT      |


#### 3️⃣ Data Relationships:  

| From Table (Column)                       | To Table (Column)                        | Relationship Type |
|------------------------------------------|------------------------------------------|-------------------|
| D_Product_Inventory(LocationID)          | D_Production_Location(LocationID)        | Many-to-One       |
| D_Product_Inventory(ModifiedDate)        | DateTable(Date)                          | Many-to-One       |
| D_Product_Inventory(ProductID)           | F_Product_Product(ProductID)             | Many-to-One       |
| D_Product_Inventory(ProductID)           | D_Product_ProductTable(ProductID)        | Many-to-One       |
| D_Production_WorkOrder(ModifiedDate)     | DateTable(Date)                          | Many-to-One       |
| D_Production_WorkOrder(ProductID)        | D_Product_ProductTable(ProductID)        | Many-to-One       |
| D_Production_WorkOrder(ProductID)        | F_Product_Product(ProductID)             | Many-to-One       |
| D_Production_WorkOrder(ScrapReasonID)    | D_Production_ScapReason(ScrapReasonID)   | Many-to-One       |
| F_Production_WorkOrderRouting(LocationID)| D_Production_Location(LocationID)        | Many-to-One       |
| F_Production_WorkOrderRouting(ProductID) | D_Product_ProductTable(ProductID)        | Many-to-One       |

<img width="783" height="509" alt="image" src="https://github.com/user-attachments/assets/6720c718-cf06-4306-a55a-9411e5608d67" />

## 🧠 Design Thinking Process  

<img width="1576" height="845" alt="image" src="https://github.com/user-attachments/assets/48ceee4d-6910-45e1-8467-8ced5e19a8bb" />

1️⃣ Empathize & EDA 

-Answer 5W1H

<img width="1024" height="645" alt="image" src="https://github.com/user-attachments/assets/ee709635-e443-4360-b2c6-31c41adec03d" />

-Put myself in the stakeholder position to create Empathy map

<img width="1034" height="767" alt="image" src="https://github.com/user-attachments/assets/fddbbf42-f5ca-4d4a-aef5-91ad6cdc2ee0" />

2️⃣ Define point of view  

-Define Northstar Metric

<img width="1040" height="762" alt="image" src="https://github.com/user-attachments/assets/68d060d7-61ec-4d9f-93ff-98373fbd87c5" />

-Define Point of View

<img width="1034" height="771" alt="image" src="https://github.com/user-attachments/assets/a8c85ec4-ce7d-4eba-b253-3bd5e476fb61" />

3️⃣ Ideate  

-BRAINSTORMING: start from Growth Formula

<img width="1034" height="754" alt="image" src="https://github.com/user-attachments/assets/92683cf3-4899-457c-bda4-e97c6e3d0736" />

## ⚒️ Main Process 

1️⃣ Data Cleaning & Preprocessing

-Delete duplicate, missing value, remove columns that unnecessary,... 

2️⃣ Exploratory Data Analysis (EDA) 

-Find the relationship between each table

-Find where is Dimtable where is Facttable

-Find which formula is necessary 

3️⃣ Create a measure table by DAX 

-Measure about quanlity, scrap, unsafe_product, value

4️⃣ Power BI Visualization

-Create a ouline 

-Choose chart or card to show the change or display indicators

## 📊 Key Insights & Visualizations  

### 🔍 Dashboard Preview  

#### 1️⃣ Dashboard 1 Preview 

- Observation: Dashboard 1 provides an overview of scrap with key metrics like Total Orders (5M), Total Scrap (1K), Scrap Value ($2.8M), and Scrap Rate (0.24%). It also highlights trends with the Top 5 locations with the highest scrap (e.g., Subassembly, Final Assembly) and Top 5 scrap products (e.g., Fork End, Seat Stays). Notable patterns include scrap reasons (e.g., Wheel misaligned, Trim too short) decreasing over the years (2011-2014), with the insight that Subassembly is the area needing the most attention.

- Recommendation: Focus on improving the Subassembly process by implementing automated inspection tools to reduce scrap. Also, prioritize monitoring and optimizing the production of products like Fork End and Seat Stays to enhance overall efficiency.

<img width="1310" height="738" alt="image" src="https://github.com/user-attachments/assets/43728426-6205-44b3-a37d-b402e2386b98" />

#### 2️⃣ Dashboard 2 Preview  

-Observation: Dashboard 2 focuses on detailed scrap analysis, showing Total Scrap by FinishedGoodsFlag (20.08K), Scrap Rate by Class (28.28% H, 37.95% M, 33.76% L), and Scrap Value per Location (peaking at $153K at Final Assembly). Trends in scrap quantity and value fluctuate (0K-2K), highlighting Final Assembly and Finished Goods Storage as areas to monitor

-Recommendation: Enhance inspections at Final Assembly and Finished Goods Storage with automated tools to reduce scrap, and conduct deeper analysis on Class M and L products to optimize processes.

<img width="1314" height="735" alt="image" src="https://github.com/user-attachments/assets/313faf5b-63d6-4f31-977a-078e43ad220b" />


#### 3️⃣ Dashboard 3 Preview

-Observation: Dashboard 3 focuses on inventory risk, showing Safety Stock (974), UnsafeProductValue ($4.66M), and distribution by location (Subassembly $2.4M, Finished Goods $2.3M). Trends indicate high unsafe products at Subassembly, requiring attention

-Recommendation: Focus on improving management at Subassembly to reduce unsafe products, implement regular inventory checks, and use forecasting tools to optimize Safety Stock.

<img width="1312" height="729" alt="image" src="https://github.com/user-attachments/assets/b8dddfe4-5e6e-4fd3-a8b2-b82efebb0e53" />


## 🔎 Final Conclusion & Recommendations  

📌 Key Takeaways:

1.🔧 Subassembly and Final Assembly are key defect points, with higher scrap rates due to inadequate inline inspection and inconsistent operator performance.

2.📦 Unsafe inventory levels are high, especially at Subassembly and Finished Goods Storage, indicating poor quality segregation and delayed decisions.

3.🧩 Certain parts—such as Fork End, Seat Stays, and Crank Sets—show up repeatedly in high-loss reports, suggesting chronic quality issues.

4.🏭 Some production lines or areas have disproportionately higher rejection rates, often due to outdated processes or lack of root cause feedback loops.

5.📊 Current dashboards mostly show surface-level trends; deeper analysis by defect reason, time, and region is essential for true problem solving.

6.💸 High-cost product classes (Class M & L) are contributing significantly to financial losses when rejected, creating a mismatch between quality risk and production value.

## ✅ Recommendations:

1. Deploy automated inspection at Subassembly and Final Assembly
Introduce AI-vision systems or sensor-based checks to identify defects early and reduce dependence on manual inspection.

2. Strengthen inventory management of unsafe and pending items
Set up clear inventory segregation rules, frequent re-check intervals, and apply forecasting models to avoid overstocking or aging quality holds.

3. Deep-dive into high-loss components like Fork End, Seat Stays
Use historical rejection data and defect reason tagging to identify failure modes and redesign or retrain processes accordingly.

4. Implement location-based quality tracking
Break down rejection and loss data by factory zone/line to spot problematic areas, and implement zone-specific SOPs or operator training.

5. Introduce a dynamic loss-cost dashboard
Go beyond quantity metrics—track actual financial loss per product category, by region and supplier, to prioritize where to act for best ROI.

6. Align production planning with quality risk
Reduce production load on lines that frequently produce high-defect products, or shift complex items to better-performing zones.



