# 📊 Power BI Product Sales Data Modeling

> **A practical data preparation, transformation, aggregation, and modeling project built with Microsoft Power BI.**

This project demonstrates an end-to-end workflow for preparing Product_Sales-related datasets in **Power Query** and organizing them in the **Power BI data model**. It covers data import, data-quality checks, transformations, calculated columns, aggregation, query merging, and relationship review.

---

## 📑 Table of Contents

- [📌 Project Overview](#-project-overview)
- [🎯 Objectives](#-objectives)
- [📁 Repository Structure](#-repository-structure)
- [🗂️ Data Sources](#️-data-sources)
- [🧹 Data Cleaning](#-data-cleaning)
- [🔄 Data Transformation](#-data-transformation)
- [🧩 Data Modeling](#-data-modeling)
- [💡 Recommendations](#-recommendations)
- [🏁 Conclusion](#-conclusion)
- [🛠️ Tools & Technologies](#️-tools--technologies)
- [📚 Key Learnings](#-key-learnings)
- [🚀 Future Improvements](#-future-improvements)
- [👤 Author](#-author)
- [🙏 Acknowledgement](#-acknowledgement)

---

## 📌 Project Overview

The purpose of this project is to practice preparing sales data for analysis and establishing relationships between datasets using Microsoft Power BI. Three CSV files were imported into Power Query Editor and prepared through a series of documented steps. The project also includes grouped summaries and a review of the data model.

| Project Detail | Description |
|---|---|
| **Project** | Power BI Product Sales Data Modeling |
| **Platform** | Microsoft Power BI Desktop |
| **Data Preparation** | Power Query Editor |
| **Source Files** | List of Orders, Order Details, Sales Target |
| **Scope** | Import, clean, transform, merge, aggregate, and model data |
| **Sample Size** | First 500 rows retained in the List of Orders query for the exercise |

---

## 🎯 Objectives

- Import multiple sales datasets into Power BI.
- Apply data preparation steps using Power Query Editor.
- Use a 500-row sample of the List of Orders query for the documented exercise.
- Apply appropriate data types to date and numeric fields.
- Standardize customer-name formatting.
- Combine City and State into a Location column.
- Calculate Profit Margin and classify Profit Status.
- Merge order-level and sales-detail data using Order ID.
- Check missing values and duplicate records.
- Sort and filter records for focused review.
- Group and aggregate data for analysis.
- Establish, inspect, and review relationships in Model View.

---

## 📁 Repository Structure

```text
📦 PowerBI_Product_Sales_Analysis
 ┣ 📂 PowerBI_Data_Modeling_Project
 ┃ ┗ 📄 PowerBI_Product_Sales_Data_Modeling.pbix
 ┣ 📂 PowerBI_Data_Modeling_Report
 ┃ ┗ 📄 PowerBI_Product_Sales_Data_Modeling_Report.pdf
 ┣ 📂 PowerBI_Product_Sales_Raw_Datasets
 ┃ ┣ 📄 List of Orders.csv
 ┃ ┣ 📄 Order Details.csv
 ┃ ┗ 📄 Sales Target.csv
 ┗ 📄 README.md
```

---

## 🗂️ Data Sources

The project uses three sales-related CSV files:

| Dataset | Power BI Query Name | Purpose |
|---|---|---|
| **List of Orders** | `Orders_List_Dataset` | Order-level details, including Order ID, Order Date, Customer Name, State, and City |
| **Order Details** | `Product_Order_Details` | Transaction details such as Amount, Profit, Quantity, Category, and Sub-Category |
| **Sales Target** | `Sales_Target_Dataset` | Target data by Category and Month of Order Date |

The query names shown above are the renamed query names documented in the project.

---

## 🧹 Data Cleaning

Data quality was reviewed in Power Query as part of the preparation process.

| Activity | Documented action |
|---|---|
| **Sample selection** | Retained the first 500 rows from the List of Orders query for this exercise. |
| **Data types** | Changed Order Date to Date and Amount and Target to Fixed Decimal Number where appropriate. |
| **Missing-value check** | Checked the reviewed tables; the report notes no missing values in the reviewed data. |
| **Duplicate check** | Identified duplicate rows and applied a duplicate-removal step to the Order Details query. |

> **Data-quality note:** Duplicate removal should be based on the meaning and grain of the records. Similar or repeated order IDs may represent legitimate order lines and should not automatically be treated as duplicate transactions.

---

## 🔄 Data Transformation

The transformations below were documented in Power Query Editor.

### 1️⃣ Text Standardization

Applied **Capitalize Each Word / Proper Case** to `CustomerName` to standardize name formatting.

### 2️⃣ 📍 Location Column

Merged `City` and `State` into a new `Location` column, using the format:

```text
City, State
```

### 3️⃣ 📈 Profit Margin

Created a custom column named `Profit Margin` using:

```powerquery
[Profit] / [Amount]
```

The column was assigned the **Percentage** data type.

### 4️⃣ 🚦 Profit Status

Created a conditional column named `Profit Status` using the following logic:

| Condition | Classification |
|---|---|
| `Profit < 0` | Loss |
| `Profit = 0` | Break-Even |
| `Profit > 0` | Profit |

### 5️⃣ 🔗 Query Merge

Merged `Orders_List_Dataset` with `Product_Order_Details` using `Order ID`. The resulting query was named **Orders Data** and the documented merge used a **Left Outer** join.

### 6️⃣ 🔍 Sorting and Filtering

- Sorted `Order Date` in descending order.
- Filtered the State field to focus on **Tamil Nadu** records for the documented example.

### 7️⃣ 📊 Data Aggregation

Grouped or duplicated queries were used to produce the following summaries:

| Summary | Grouping Field | Aggregation |
|---|---|---|
| Count of Order ID | Order ID | Count Rows |
| Average Profit by Category | Category | Average of Profit |
| Total Amount by Sub-Category | Sub-Category | Sum of Amount |
| Total Target by Month of Order Date | Month of Order Date | Sum of Target |

These summaries illustrate how detailed records can be organized into grouped tables for further analysis.

---

## 🧩 Data Modeling

Relationships were created and reviewed in Power BI using **Manage Relationships** and **Model View**.

### 🔗 Relationships

| Tables | Relationship Key | Cardinality shown in the project |
|---|---|---|
| `Orders_List_Dataset` ↔ `Product_Order_Details` | `Order ID` | One-to-one (1:1) |
| `Product_Order_Details` ↔ `Sales_Target_Dataset` | `Category` | Many-to-many (*:*) |

These relationships as active, with cross-filter direction set to **Both**.

### 🧪 Model Review

- Reviewed relationship keys and cardinality.
- Checked relationship activation and settings through Manage Relationships.
- Inspected the connected tables in Model View.

> **Model design consideration:** Validate cardinality and filter direction against the full dataset before using the model for reporting. Many-to-many relationships and bidirectional filtering can lead to ambiguity or unexpected filtering. A future model could use shared dimension tables (such as Date and Category) and one-to-many relationships where the data supports them.

---

## 💡 Recommendations

- **Validate relationship design:** Confirm key uniqueness, cardinality, and filter direction using the full datasets.
- **Consider a star schema:** Introduce shared dimensions such as Date and Category, where appropriate, to improve model clarity and maintainability.
- **Develop reusable DAX measures:** Build measures for Amount, Profit, Profit Margin, Order Count, and Target Achievement.
- **Expand analytical views:** Compare performance by category, sub-category, location, and time.
- **Maintain data-quality documentation:** Record cleaning rules, assumptions, and any changes to source records.
- **Validate beyond the sample:** Recheck transformation and model results against the complete dataset before drawing business conclusions.

---

## 🏁 Conclusion

This project demonstrates a practical Power BI workflow for preparing and modeling sales-related data. It covers importing multiple CSV datasets, applying cleaning and transformation steps in Power Query, creating custom and conditional columns, merging queries, generating grouped summaries, and reviewing relationships in Model View.

The project provides a foundation for further reporting and analysis. Validating the model against the full datasets, improving the relationship design where necessary, and creating reusable DAX measures would support the development of a more robust analytical solution.

---

## 🛠️ Tools & Technologies

| Tool | Usage |
|---|---|
| **Microsoft Power BI Desktop** | Data import, model review, and project development |
| **Power Query Editor** | Data cleaning, transformation, merging, filtering, and grouping |
| **CSV** | Source data format |
| **Model View** | Visual inspection of table relationships |
| **Manage Relationships** | Review and configure relationship settings |

---

## 📚 Key Learnings

- Importing and managing multiple CSV datasets in Power BI.
- Using Power Query and Applied Steps to prepare data.
- Applying row sampling and data-type management.
- Standardizing text and combining columns.
- Creating custom and conditional columns.
- Merging queries with key fields and join types.
- Checking missing values and duplicate records.
- Sorting, filtering, grouping, and aggregating data.
- Understanding relationship cardinality and cross-filter direction.
- Reviewing model structure using Model View and Manage Relationships.

---

## 🚀 Future Improvements

- Extend the exercise beyond the 500-row sample and validate against the full dataset.
- Create a dedicated Date table and other shared dimensions as appropriate.
- Reassess relationship cardinality and filter direction to reduce ambiguity.
- Develop DAX measures for Sales, Profit, Profit Margin, Order Count, and Target Achievement.
- Build an interactive report with KPI cards, charts, drill-downs, and slicers.
- Add more systematic data-quality checks and document assumptions.
- Test model behavior and measure accuracy against independently calculated results.

---

## 👤 Author

**Manikandan S**

Aspiring Data Analyst | Learning Excel, Power BI and developing practical data analysis projects.

- 🔗 LinkedIn: https://www.linkedin.com/in/manikandan042/
- 💻 GitHub: https://github.com/ManikandanSuriyakumar
- 📧 Email: manisuriyakumar042@gmail.com

---

## 🙏 Acknowledgement

This project was developed as a hands-on learning exercise to demonstrate data preparation, transformation, aggregation, and modeling workflows in Microsoft Power BI using Product_Sales-related datasets and Data Models.

---

⭐ If you found this project helpful, consider giving the repository a star!
