# Total Facilities That Sell the Product

## Business Problem

Retailers need visibility into how many and which facilities (stores, warehouses, or virtual sites) currently offer a product for sale. This helps in stock management and planning.

## Fields to Retrieve

The query retrieves the following details:

- `PRODUCT_ID`
- `PRODUCT_NAME` (or `INTERNAL_NAME`)
- `FACILITY_COUNT` (Number of facilities selling the product)
- `FACILITY_IDS` (A concatenated list of facility IDs offering the product, if needed)

## SQL Query

```sql
SELECT
    P.PRODUCT_ID,
    P.PRODUCT_NAME,
    COUNT(II.FACILITY_ID) AS FACILITY_COUNT,
    GROUP_CONCAT(II.FACILITY_ID) AS FACILITY_IDS
FROM INVENTORY_ITEM II
LEFT JOIN PRODUCT P
ON P.PRODUCT_ID = II.PRODUCT_ID
GROUP BY P.PRODUCT_ID;
```

## Query Explanation

1. **Query `INVENTORY_ITEM` table**: Retrieves the facilities where each product is available.
2. **Join with `PRODUCT` table**: Fetches product names for reference.
3. **Apply `COUNT(II.FACILITY_ID)`**: Determines the number of facilities selling each product.
4. **Use `GROUP_CONCAT(II.FACILITY_ID)`**: Optionally lists all facility IDs selling a product.
5. **Group by `PRODUCT_ID`**: Ensures aggregation is done at the product level.

## Query Cost

- Estimated query cost: **4,124,358.58**  
- Expected rows retrieved: **1,955,525**
