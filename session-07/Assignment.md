# Session 07 Assignment: SQL & SQLite Queries

## Setup Instructions

Load the following Olist dataset CSV files into your SQLite database using these **exact** table names:

- `orders` (from `olist_orders_dataset.csv`)
- `order_items` (from `olist_order_items_dataset.csv`)
- `products` (from `olist_products_dataset.csv`)
- `reviews` (from `olist_order_reviews_dataset.csv`)

---

## Assignment Questions

Write the SQL query to answer each question below:

1. **Distinct Statuses:** Find the distinct list of status updates in the `orders` table.
2. **Price Summary:** Find the minimum, average, and maximum price of items sold in the `order_items` table.
3. **Delivered Orders:** Count how many orders have been marked as `'delivered'`.
4. **Low Review Ratings:** Write a join to return the `product_id`, `product_category_name`, and `review_score` for items that received a review score of `1`.
5. **High-Value Categories:** Find all product categories with an average purchase price above $150.
6. **Average Freight:** Find the average freight cost (`freight_value`) in `order_items`.
7. **Top 5 Prices:** List the top 5 highest-priced items in `order_items` (display `order_id` and `price`, ordered from highest to lowest).
8. **Specific Order Category Lookup:** Join `order_items` and `products` to get the category name for `order_id = '00010242fe8c5a6d1ba2dd792cb16214'`.
9. **Review Score Distribution:** Show the distribution of reviews (`review_score` and count) grouped by score, where `review_score` is `NOT NULL`.
10. **Category Max Price:** Find the maximum price of a product sold in the `'cool_stuff'` category.
