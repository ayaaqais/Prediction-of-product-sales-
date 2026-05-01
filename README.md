# Predicting Retail Product Sales to Drive Business Growth

## Using Machine Learning to Help Retailers Identify the Key Drivers of Sales Performance

**Author: Aya Khalil**

---

## Business Problem

Retailers carry thousands of products across dozens of outlets, yet only a fraction of them drive the majority of revenue. Without data-driven guidance, decisions about which products to stock, how to price them, and which stores to invest in are made on instinct alone.

This project builds a machine learning model to **predict the sales (`Item_Outlet_Sales`) of food products across retail outlets**, enabling the retailer to:

- Identify which product and outlet characteristics drive the highest sales
- Prioritize high-revenue products and outlet types for investment
- Make data-backed decisions about inventory, pricing, and store expansion

---

## Data

**Source:** Big Mart Sales Dataset  
**Size:** 8,523 products × 12 features  
**Target Variable:** `Item_Outlet_Sales` — the sales revenue of a product at a specific outlet

| Feature | Description |
|---|---|
| Item_MRP | Maximum Retail Price (list price) of the product |
| Item_Type | The product category (e.g., Dairy, Snack Foods, Frozen Foods) |
| Outlet_Type | Whether the outlet is a Grocery Store or Supermarket (Types 1–3) |
| Outlet_Size | Physical size of the store (Small, Medium, High) |
| Outlet_Location_Type | Area type — Tier 1 (metro), Tier 2, or Tier 3 (small town) |
| Item_Visibility | % of total store display area allocated to the product |
| Item_Weight | Weight of the product (kg) |
| Item_Fat_Content | Low Fat or Regular |

---

## Methods

**Data Preparation:**
- Removed duplicate records to ensure clean training data
- Standardized inconsistent category labels in `Item_Fat_Content` (e.g., 'LF' → 'Low Fat')
- Dropped `Item_Identifier` due to its extremely high cardinality (1,559 unique IDs) which provides no generalizable signal
- Applied `SimpleImputer` (mean strategy) for the 17.2% missing values in `Item_Weight`
- Applied `SimpleImputer` (most frequent strategy) for the 28.3% missing values in `Outlet_Size`
- Used `StandardScaler` to normalize all numeric features
- Used `OneHotEncoder` to convert categorical variables into model-ready numeric format
- Split data into 80% training / 20% test sets *before* any imputation or scaling to prevent data leakage

**Modeling Approach:**
Built and compared three models using scikit-learn Pipelines:
1. Linear Regression (baseline)
2. Random Forest — default parameters
3. Random Forest — tuned with GridSearchCV (`n_estimators`, `max_depth`, `min_samples_split`)

---

## Key Insights

### Insight 1: Product Price is the Strongest Predictor of Sales

![MRP vs Sales](/insight1_mrp_vs_sales.png)

> There is a clear positive relationship between a product's Maximum Retail Price (MRP) and its sales revenue (Pearson correlation ≈ 0.57). Higher-priced items consistently generate more revenue — making Item_MRP the most important numeric feature in the model. Retailers should ensure premium products receive appropriate shelf space and visibility.

---

### Insight 2: Outlet Type is the #1 Driver of Sales Performance

![Outlet Type vs Sales](/insight2_outlet_type_vs_sales.png)

> Supermarket Type 3 outlets dramatically outperform all other outlet types, with median sales nearly **3× higher** than Grocery Stores. The type of outlet a product is sold in matters more than almost any product-level attribute. This finding strongly supports investing in Supermarket Type 3 expansion to maximize total revenue.

---

## Model

**Final Recommended Model: Tuned Random Forest Regressor**

A Random Forest was chosen over Linear Regression because it captures non-linear relationships (e.g., between price tiers and sales) and handles feature interactions automatically (e.g., how Outlet Type interacts with Item MRP).

GridSearchCV was used to tune `n_estimators`, `max_depth`, and `min_samples_split` across 5-fold cross-validation to reduce overfitting while maximizing generalization.

### Model Performance

| Model | Training R² | Test R² | Test RMSE |
|---|---|---|---|
| Linear Regression | 0.5595 | 0.5793 | $1,069 |
| Random Forest (Default) | 0.9376 | 0.5705 | $1,080 |
| **Random Forest (Tuned) ** | **0.8888** | **0.5763** | **$1,073** |

### What do these numbers mean for the business?

The tuned model explains approximately **58% of the variation in product sales** across outlets. In practical terms, the model's predictions are off by an average of **~$1,073 per product** ,roughly 8% of the average sale value.

The **RMSE** metric was selected as the primary business metric because it is expressed in dollars (the same unit as sales), making it intuitive for non-technical stakeholders. It also penalizes large prediction errors more than MAE, which is important for avoiding badly wrong forecasts on high-value products.

The tuned model shows **moderate overfitting** (Train R² = 0.89 vs Test R² = 0.58). This gap was reduced significantly through GridSearch tuning (from 0.37 in the default RF down to 0.31), indicating the tuning was effective. Further improvement requires additional data or features.

---

## Recommendations

1. **Prioritize Supermarket Type 3 outlets** for product placement and store expansion, they generate the highest sales by a wide margin.

2. **Focus marketing and shelf space on higher-MRP products**, price is the strongest predictor of revenue and should guide inventory allocation decisions.

3. **Investigate Grocery Stores separately**, their significantly lower sales may reflect a fundamentally different customer base that warrants its own pricing and product strategy.

---

## Limitations & Next Steps

**Current limitations:**
- The model explains ~58% of sales variance; 42% is driven by factors not in the dataset (promotions, seasonality, local competition, foot traffic)
- Moderate overfitting remains — the model performs better on training data than on new data

**Recommended next steps:**
- Collect additional features: promotional history, foot traffic data, local competitor density, and seasonal/time-series information
- Engineer new features: product age, outlet age (2023 − Establishment Year), MRP price tier categories
- Experiment with Gradient Boosting models (XGBoost, LightGBM) which are known to outperform Random Forests on tabular retail data
- Re-evaluate model quarterly as new sales data becomes available

---

### For Further Information

For any additional questions, please contact **ayaaqaiss@gmail.com**

*Full technical details, data preparation steps, and all model code are available in the project notebook.*
