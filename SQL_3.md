# Product Threshold Value

## Business Problem

The retailer has set a threshold value for products that are sold online to prevent overselling and ensure stock availability.

## Fields to Retrieve

The query retrieves the following details related to product threshold values:

- `PRODUCT_ID`
- `FACILITY_ID`
- `FACILITY_NAME`
- `FACILITY_TYPE_ID`
- `THRESHOLD (MINIMUM_STOCK)`

## SQL Query

```sql
SELECT
    PFC.PRODUCT_ID,
    PFC.FACILITY_ID,
    F.FACILITY_NAME,
    F.FACILITY_TYPE_ID,
    PFC.MINIMUM_STOCK
FROM PRODUCT_FACILITY PFC
JOIN FACILITY F
ON PFC.FACILITY_ID = F.FACILITY_ID
WHERE PFC.MINIMUM_STOCK > 0;
```

## Query Explanation

To retrieve the product threshold values:

1. **Query `PRODUCT_FACILITY` table**: Retrieves the minimum stock values for products.
2. **Join with `FACILITY` table**: Fetches facility-related details like name and type.
3. **Apply filter `MINIMUM_STOCK > 0`**: Ensures only products with a defined threshold are included in the result.

## Query Cost:
444,000 (1,444,000 rows)

