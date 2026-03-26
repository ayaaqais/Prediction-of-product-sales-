# Prediction of Product Sales

## Project Overview
This project uses pyton libraries( pandas, numpy, matplotlip, seaborn) to predict product sales.
The dataset contains information about products and outlets.
The goal is to understand what factors drive Item_Outlet_Sales.

## Dataset

| Column | Description |
|--------|-------------|
| Item_Identifier | unique ID for each product |
| Item_Weight | Weight of the product |
| Item_Fat_Content | Fat content of the product (Low Fat or Regular) |
| Item_Visibility | Percentage of display area allocated to the product (0 to 1) |
| Item_Type | Product category e.g. (Dairy, Snacks, Beverages) |
| Item_MRP | Maximum Retail Price of the product |
| Outlet_Identifier | unique ID for each store |
| Outlet_Establishment_Year | year the store was opened |
| Outlet_Size | Size of the store (Small, Medium, or High) |
| Outlet_Location_Type | City tier where the store is located (Tier 1, 2, or 3) |
| Outlet_Type | Type of store (grocery Store or Supermarket Type 1/2/3) |
| Item_Outlet_Sales | Target (total sales of the product in the store) |

## Project Steps

1. Load & Inspect Data
2. Clean Data
3. Exploratory Data Analysis (EDA)
4. Modeling (Upcoming)


### 1. Histogram for Item_MRP

<img width="1172" height="744" alt="histo_item_mrp" src="https://github.com/user-attachments/assets/5d8b69be-2d3c-4870-8b3a-42e79d31a1f3" />

Products are spread across four clear price ranges, suggesting that
items are grouped into pricing tiers rather than priced freely.

### 2. Heatmap — Correlation

<img width="952" height="644" alt="heatmap" src="https://github.com/user-attachments/assets/145f675f-6efb-423b-905f-7a0a2140c525" />

Item_MRP has the strongest positive correlation with Item_Outlet_Sales (0.57),
meaning higher-priced products tend to generate more revenue.

## How to Run

1. Upload the CSV to Colab
2. Open the notebook
3. Run all cells

## Author
Aya Khalil
