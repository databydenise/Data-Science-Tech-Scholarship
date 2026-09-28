# Assignment 5: Multi-Table Data Quality Audit & Metric Visualization

## Overview & Instructions
In this assignment, you will evaluate data quality issues across four core tables from the Olist E-commerce dataset. You will load the datasets into Google Colab, write Pandas code to calculate exact quality metrics, visualize underlying distribution anomalies using Seaborn/Matplotlib, and document defensible treatment strategies for each issue.

### Dataset Setup
In your Colab notebook, load the following four datasets using Pandas and assign them to these exact variable names:
- `orders` $\rightarrow$ `olist_orders_dataset.csv`
- `order_items` $\rightarrow$ `olist_order_items_dataset.csv`
- `reviews` $\rightarrow$ `olist_order_reviews_dataset.csv`
- `products` $\rightarrow$ `olist_products_dataset.csv`

---

## Part A: Defensible Data Quality Audit (5-Point Analysis)

For each of the five issues below, write and execute the Pandas code in the designated code cell to calculate the requested quality metrics and confirm the issue.

---

### Issue 1: Missing Temporal Timestamps in Orders

* **Dataset & Column:** `orders` (`olist_orders_dataset.csv`) $\rightarrow$ `order_delivered_customer_date`
* **Data Quality Dimension Violated:** Completeness
* **Evidence & Summary Metrics:** Run code to find how many records are missing customer delivery dates. Note that about 3% of orders are missing this timestamp.
* **Business & Analytical Impact:** If left uncleaned, calculations for overall average delivery times will be biased. Delayed or failed orders will be omitted, making logistics performance look better than it actually is.
* **Defensible Cleaning Plan:** Create a flag column `is_delivered` (`True`/`False`). If order status is `'delivered'` but delivery date is null, flag it for data integrity verification and isolate these records in reporting. Do not blindly impute with average dates.

---

### Issue 2: Extreme Outliers in Product Prices

* **Dataset & Column:** `order_items` (`olist_order_items_dataset.csv`) $\rightarrow$ `price`
* **Data Quality Dimension Violated:** Validity (Range & Distribution)
* **Evidence & Summary Metrics:** Max price is $6,735.00 while the median is only $74.90. Highly skewed distribution (Skewness index > 7.0).
* **Business & Analytical Impact:** Predictive models like regression are heavily influenced by extreme values, which leads to skewed sales forecasts and pricing optimization policies.
* **Defensible Cleaning Plan:** Keep the outliers in the transactional database, but apply a robust scaler (like robust scaling with IQR) or a log transformation for machine learning algorithms. Do not drop these rows, as they represent actual high-value transactions.


---

### Issue 3: Missing Catalog Product Categories

* **Dataset & Column:** `products` (`olist_products_dataset.csv`) $\rightarrow$ `product_category_name`
* **Data Quality Dimension Violated:** Completeness
* **Evidence & Summary Metrics:** 610 products do not have a registered category name.
* **Business & Analytical Impact:** This breaks inventory planning and marketing analysis, making it impossible to correctly group sales performance by category.
* **Defensible Cleaning Plan:** Group missing values and map them to a new category label called `'unclassified'`. This preserves transaction records for revenue analysis while preventing categorical modeling errors.

---

### Issue 4: Duplicate Review Submissions Across Orders

* **Dataset & Column:** `reviews` (`olist_order_reviews_dataset.csv`) $\rightarrow$ `review_id`
* **Data Quality Dimension Violated:** Consistency / Integrity
* **Evidence & Summary Metrics:** Multiple orders share the exact same `review_id`, resulting in duplication during joins.
* **Business & Analytical Impact:** Joining datasets on duplicate keys multiplies transaction records. This artificially inflates overall revenue numbers and customer feedback metrics in reports.
* **Defensible Cleaning Plan:** Deduplicate the reviews dataset before joining by keeping only the latest review submission based on the review timestamp, or group the reviews to map them cleanly.

---

### Issue 5: Products Catalogued with 0 Grams of Weight

* **Dataset & Column:** `products` (`olist_products_dataset.csv`) $\rightarrow$ `product_weight_g`
* **Data Quality Dimension Violated:** Accuracy
* **Evidence & Summary Metrics:** 4 products are listed with a weight of exactly 0g.
* **Business & Analytical Impact:** Standard automated freight calculators will return shipping cost estimates of zero. This causes financial losses when fulfilling shipments.
* **Defensible Cleaning Plan:** Find similar products in the database using their category and dimensions, and impute the median weight of those matches. Alternatively, replace the values with the overall median weight of that specific product category.

---

## Part B: Practical Visualization Recall

We will write clean, well-structured visualization code using Seaborn and Matplotlib to analyze and confirm your data quality findings from Part A.

### Task 1: Price Distribution & Outliers

Create a composite figure showing a boxplot and a distribution plot (KDE/histogram) of `price` from `order_items` to visually highlight extreme right-skewed outliers.


---

### Task 2: Order Status Breakdown

Create a Seaborn bar plot showing the counts of different `order_status` values in the `orders` dataset to observe non-delivered order volumes.

---

## Part C: Written Reflection

In the space below, write 2–3 paragraphs addressing the following points:

1. **Numerical vs. Visual Auditing:** What did your visual plots in Part B reveal about the data quality issues that simple summary numbers like `.isnull().sum()` or `.describe()` did not fully convey?
2. **Defensible Business Decisions:** Why is blindly running `df.dropna()` or dropping all statistical outliers dangerous in an e-commerce context? Support your explanation using one of the five issues audited above.

