# Completed Orders in August 2023

## Business Problem

After running similar reports for a previous month, you now need all completed orders in August 2023 for analysis.

## Fields to Retrieve

The query retrieves the following details for completed orders in August 2023:

- `PRODUCT_ID`
- `PRODUCT_TYPE_ID`
- `PRODUCT_STORE_ID`
- `TOTAL_QUANTITY`
- `INTERNAL_NAME`
- `FACILITY_ID`
- `EXTERNAL_ID`
- `FACILITY_TYPE_ID`
- `ORDER_HISTORY_ID`
- `ORDER_ID`
- `ORDER_ITEM_SEQ_ID`
- `SHIP_GROUP_SEQ_ID`

## SQL Query

```sql
SELECT 
    OH.ORDER_ID,
    OH.STATUS_ID,
    OH.EXTERNAL_ID,
    OH2.ORDER_HISTORY_ID,
    OI.ORDER_ITEM_SEQ_ID,
    OI.QUANTITY,
    P.PRODUCT_ID,
    P.PRODUCT_TYPE_ID,
    P.INTERNAL_NAME,
    OSG.SHIP_GROUP_SEQ_ID,
    F.FACILITY_ID,
    F.FACILITY_TYPE_ID,
    F.PRODUCT_STORE_ID
FROM ORDER_HEADER OH
JOIN ORDER_STATUS OS
ON OS.STATUS_ID = 'ORDER_COMPLETED'
AND OS.ORDER_ID = OH.ORDER_ID
AND OS.STATUS_DATETIME BETWEEN '2023-08-01' AND '2023-08-31'
JOIN ORDER_HISTORY OH2
ON OH.ORDER_ID = OH2.ORDER_ID
JOIN ORDER_ITEM OI
ON OI.ORDER_ITEM_SEQ_ID = OH2.ORDER_ITEM_SEQ_ID
AND OI.ORDER_ID = OH2.ORDER_ID
JOIN PRODUCT P
ON OI.PRODUCT_ID = P.PRODUCT_ID
JOIN ORDER_ITEM_SHIP_GROUP OSG
ON OH2.SHIP_GROUP_SEQ_ID = OSG.SHIP_GROUP_SEQ_ID
AND OH2.ORDER_ID = OSG.ORDER_ID
JOIN FACILITY F
ON OSG.FACILITY_ID = F.FACILITY_ID
GROUP BY OH.ORDER_ID;
```

## Query Explanation

To retrieve all completed orders in August 2023:

1. **Join `ORDER_HEADER` and `ORDER_STATUS`**: Ensures only orders with status `ORDER_COMPLETED` within the specified date range are included.
2. **Join `ORDER_HISTORY`**: Captures the history of order changes.
3. **Join `ORDER_ITEM`**: Retrieves specific details about ordered products, including quantity and product type.
4. **Join `PRODUCT`**: Fetches product details such as name and type.
5. **Join `ORDER_ITEM_SHIP_GROUP`**: Links shipping details to the order.
6. **Join `FACILITY`**: Retrieves information about the facility handling the order.
