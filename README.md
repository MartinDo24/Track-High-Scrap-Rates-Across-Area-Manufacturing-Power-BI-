# Production-process-analysis

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/b4e8804a-dae3-4140-b75c-309c75654c28" />

Author: ĐỖ HOÀNG MINH  

Date: 2025-05-05  

Tools Used: Power BI  

## 📑 Table of Contents 

1.[📌 Background & Overview](#-background--overview)  

2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  

3. [🧠 Design Thinking Process](#-design-thinking-process)

4. [📊 Key Insights & Visualizations](#-key-insights--visualizations)

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

## 📂 Dataset Description & Data Structure  

### 📌 Data Source  

- Source: Used the data already in the PBIX file to make reports

- Size: 8 columns ~ 100K rows

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

1️⃣ Empathize & EDA 

-Answer 5W1H

<img width="1016" height="360" alt="image" src="https://github.com/user-attachments/assets/183e77b6-4ff2-437b-9fe6-fa9b5555d7ca" />

-Put myself in the stakeholder position to create Empathy map

<img width="625" height="402" alt="image" src="https://github.com/user-attachments/assets/5b464ea0-e4ea-4231-aa12-66b2a0c4310e" />

-EDA 

<img width="272" height="381" alt="image" src="https://github.com/user-attachments/assets/989fd89f-3dcc-47c3-88e5-72617b93f8d9" />

2️⃣ Define point of view  

-Define Northstar Metric

<img width="239" height="359" alt="image" src="https://github.com/user-attachments/assets/13f66c35-2368-4767-b2c0-1bf1e955e082" />

-Define Point of View

<img width="459" height="351" alt="image" src="https://github.com/user-attachments/assets/84ad77b2-8903-4be6-8581-ab63367af58d" />

-Create some Growth Formula base on Pov 

<img width="625" height="121" alt="image" src="https://github.com/user-attachments/assets/023edd51-c8e2-4345-93f0-d1f4689db72a" />

3️⃣ Ideate  

-BRAINSTORMING: start from Growth Formula

<img width="652" height="403" alt="image" src="https://github.com/user-attachments/assets/066cfe88-80d5-403b-9534-947bf4dc49c8" />

-STRUCTURE IDEA: start from each Pov

<img width="922" height="294" alt="image" src="https://github.com/user-attachments/assets/63fb52fc-eff7-4893-a578-fe5ad8822b12" />




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

✔️ Recommendation 1: Focus on improving processes at Subassembly and Final Assembly with automated inspection tools to effectively reduce scrap.

✔️ Recommendation 2: Enhance management of unsafe inventory at Subassembly and Finished Goods Storage, using regular checks and forecasting to optimize Safety Stock.

✔️ Recommendation 3: Prioritize optimizing production of key products like Fork End, Seat Stays, and conduct deeper analysis on product classes (Class M, L) to improve overall efficiency.



