## Assignment


1. **Load Datasets:** 
   * Open **Power BI Desktop**.
   * Select **Get Data** ➡️ **Text/CSV**.
   * Import `olist_sales_master.csv`.
   * Import `olist_reviews_master.csv`.
2. **Transform your data:**
   * Make sure BI assigns the correct data types to different columns.
2. **Inspect Relationships:**
   * Navigate to the **Model View** tab.
   * Verify that both tables are treated as independent fact tables. If you want to analyze reviews alongside product sales, link both tables on the common key `order_id` as a **1-to-Many** relationship (or keep them separate to preserve clean granularity!).
3. **Create your visuals:**
   * Pick the appropriate charts to answer the questions below. Paginate accordingly
   

---

### 👥 Group A: Sales and Product Performance

#### Question 1: Which Brazilian state generates the highest total sales volume (revenue)?
* **Caution:** Remember that `price` represents the cost of the *item line* and excludes the freight cost. To find overall customer checkout costs, you must combine `price` and `freight_value`

#### Question 2: What are the top 10 product categories by item count, and do they also generate the most revenue?


#### Question 3: How does the number of unique orders scale on a monthly trend, and is there visible seasonality?
* **Caution:** A basic count of rows will represent item counts rather than orders. Ensure you set the calculation aggregation type to **Distinct Count**!

---

### 👥 Group B: Customer Experience and Deliveries

#### Question 1: Which customer states suffer from the lowest average customer review scores?
* **Caution:** Power BI defaults to **Sum** on numeric fields. You must explicitly click the drop-down on the `review_score` field in the Values bucket and change it to **Average**.

#### Question 2: What is the overall distribution of satisfaction scores across all transactions?

#### Question 3: Is there a visible relationship between delivery delays and customer satisfaction?
