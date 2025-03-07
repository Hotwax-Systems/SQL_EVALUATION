### 5.2 Orders from New York

**Business Problem:**  
Companies often want region-specific analysis to plan local marketing, staffing, or promotions in certain areas—here, specifically, New York.

**Fields to Retrieve:**  
- `ORDER_ID` 
- `CUSTOMER_NAME` 
- `STREET_ADDRESS` (or shipping address detail)  
- `CITY`  
- `STATE_PROVINCE`
- `POSTAL_CODE` 
- `TOTAL_AMOUNT`
- `ORDER_DATE`  
- `ORDER_STATUS`

# Orders from New York

## Business Problem

Companies often require region-specific analysis to optimize local marketing, staffing, and promotions. This query focuses on retrieving orders placed in New York for such analysis.

## Fields to Retrieve

The query retrieves the following details for orders from New York:

- `ORDER_ID`
- `CUSTOMER_NAME`
- `STREET_ADDRESS` (or shipping address detail)
- `CITY`
- `STATE_PROVINCE`
- `POSTAL_CODE`
- `TOTAL_AMOUNT`
- `ORDER_DATE`
- `ORDER_STATUS`

## SQL Query

```sql
SELECT
    O.ORDER_ID,
    C.FIRST_NAME || ' ' || C.LAST_NAME AS CUSTOMER_NAME,
    A.STREET_ADDRESS,
    A.CITY,
    A.STATE_PROVINCE,
    A.POSTAL_CODE,
    O.TOTAL_AMOUNT,
    O.ORDER_DATE,
    O.ORDER_STATUS
FROM ORDER_HEADER O
JOIN CUSTOMER C ON O.CUSTOMER_ID = C.CUSTOMER_ID
JOIN ADDRESS A ON O.SHIPPING_ADDRESS_ID = A.ADDRESS_ID
WHERE A.STATE_PROVINCE = 'New York';
```

## Query Explanation

1. **Join `ORDER_HEADER` and `CUSTOMER`**: Retrieves order details along with the customer’s full name.
2. **Join `ADDRESS` table**: Fetches the shipping address details including city, state, and postal code.
3. **Filter by `STATE_PROVINCE = 'New York'`**: Ensures only orders from New York are included.

## Query Cost
30,000 (11,000 rows)
