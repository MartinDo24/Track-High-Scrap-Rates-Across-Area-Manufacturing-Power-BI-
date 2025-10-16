# Track High Scrap Rates Across Area  – Manufacturing | Power BI 


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

Which products have the highest defect rate? Which areas incur the most loss? Which suppliers are underperforming?

✅Addresses scrap issues for E-commerce company by identifying key locations and causes of waste

✅Reduces unsafe inventory risks through safety management and data analysis

✅Improves production efficiency by suggesting tools and processes to optimize quality

✅Find out areas have most scrap rate

### 👤 Who is this project for?  

-Production director

-Strategic planners

-Data analysts



## 📂 Dataset Description & Data Structure  

### 📌 Data Source  

- Source: Used the data already in the PBIX file to make reports

- Size: 8 table ~ 100K rows

- Format: Production-process-analysis.pbix


### 📊 Data Structure & Relationships  

<details>
<summary>1️⃣ Tables Used:</summary>

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

</details>

<details>
<summary> 2️⃣ Table Schema & Data Snapshot </summary>  

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


</details>

<details>
<summary> 3️⃣ Data Relationships: </summary>  

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

</details>

## 🧠 Design Thinking Process  


1️⃣ Empathize & EDA 

-Answer 5W1H

<img width="1032" height="746" alt="image" src="https://github.com/user-attachments/assets/46794a08-8087-4d09-b747-7cd788c1e349" />

-Put myself in the stakeholder position to create Empathy map

<img width="1063" height="734" alt="image" src="https://github.com/user-attachments/assets/5f2a981e-373e-44c9-bebd-a41db6e63937" />

2️⃣ Define point of view  

-Define Northstar Metric

<img width="1375" height="515" alt="image" src="https://github.com/user-attachments/assets/4ba86840-be83-47bc-a34e-f4be0ffc6735" />

-Brainstorming

<img width="1059" height="591" alt="image" src="https://github.com/user-attachments/assets/e2a90dfa-0fe1-466c-ba25-ea1ca9b6b254" />

3️⃣ Ideate  

<img width="1035" height="730" alt="image" src="https://github.com/user-attachments/assets/bac59153-cc75-4564-9e2b-3627f589e34c" />


# Build dashbroad
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

- Observation: Dashboard 1 provides an overview of scrap with key metrics like Total Orders (5M), Total Scrap (1K), Scrap Value ($2.8M), and Scrap Rate (0.24%). It also highlights trends with the Top 5 locations with the highest scrap (e.g., Subassembly, Final Assembly) and Top 5 scrap products (e.g., Fork End, Seat Stays). ML Crankset was a highest product scrap especially in Jun 2012 and July 2013, total scrap was 225 and highest in 20133 with 139 and the common reason scrap was Thermoform temperature too low, color incorrect . 

- Recommendation: Need to re-check the machinery system and assembly team at the final assembly stage, especially for the ML crankset product when this product alone has a deficit of $25.6K

<img width="1313" height="736" alt="image" src="https://github.com/user-attachments/assets/a581b318-84a4-447b-bebb-dc8b08da574f" />

#### 2️⃣ Dashboard 2 Preview  

-Observation: Dashboard 2 focuses on detailed scrap analysis, showing Total Scrap by FinishedGoodsFlag (20.08K), Scrap Rate by Class (28.28% H, 37.95% M, 33.76% L), and Scrap Value per Location (peaking at $153K at Final Assembly). Trends in scrap quantity and value fluctuate (0K-2K), highlighting Final Assembly and Finished Goods Storage as areas to monitor. 

-Recommendation: Scrap products leading to cost deficits usually occur from late June to September, which is the peak season for sales due to the summer and requires additional staffing during this time, as well as increased process monitoring and inspection, especially in the final assembly area, where $166K has been spent. At the same time, focus more on class M because this is a popular segment with many buyers, but it is noted that this product also has many errors due to the reason Thermoform temperature too low.

<img width="1313" height="737" alt="image" src="https://github.com/user-attachments/assets/07b51f5c-d274-4532-b97a-e9d8f77ce691" />

#### 3️⃣ Dashboard 3 Preview

-Observation: Dashboard 3 focuses on inventory risk, showing Safety Stock (974), UnsafeProductValue ($4.66M), and distribution by location (Subassembly $2.4M, Finished Goods $2.3M). Trends indicate high unsafe products at Subassembly, requiring attention

-Recommendation: Road-150 Red, 44 at Final Assembly which has unsafe value highest can be the potential to threaten revenue, need to review or eliminate this product to avoid unnecessary loss or optimize, redesign the product

<img width="1313" height="740" alt="image" src="https://github.com/user-attachments/assets/cde11526-5809-4fba-b25d-606540c9dc41" />

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



