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
select
	OH.ORDER_ID ,
	OH.ORDER_DATE ,
	OH.STATUS_ID ,
	OR2.PARTY_ID ,
	OR2.ROLE_TYPE_ID ,
	PER.FIRST_NAME AS CUSTOMER_FIRST_NAME,
	PER.LAST_NAME AS CUSTOMER_SECOND_NAME,
	PG.GROUP_NAME AS ORGANIZATION,
	OH.GRAND_TOTAL as TOTAL_AMOUNT,
	PA.ADDRESS1 AS STREET_ADDRESS,
	PA.CITY
FROM
	ORDER_HEADER OH
JOIN ORDER_ROLE OR2
ON
	OH.ORDER_ID = OR2.ORDER_ID
	AND OR2.ROLE_TYPE_ID = 'PLACING_CUSTOMER'
LEFT JOIN PERSON PER
ON
	PER.PARTY_ID = OR2.PARTY_ID
LEFT JOIN PARTY_GROUP PG
ON
	PG.PARTY_ID = OR2.PARTY_ID
JOIN ORDER_CONTACT_MECH OCM
ON
	OCM.ORDER_ID = OH.ORDER_ID
	AND OCM.CONTACT_MECH_PURPOSE_TYPE_ID = 'SHIPPING_LOCATION'
 JOIN POSTAL_ADDRESS PA
ON
	PA.CONTACT_MECH_ID = OCM.CONTACT_MECH_ID and PA.CITY = 'New York'

```

## Query Explanation

1. **Join `ORDER_HEADER` and `CUSTOMER`**: Retrieves order details along with the customer’s full name.
2. **Join `ADDRESS` table**: Fetches the shipping address details including city, state, and postal code.
3. **Filter by `STATE_PROVINCE = 'New York'`**: Ensures only orders from New York are included.

## Query Cost
30,000 (11,000 rows)
