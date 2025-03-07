# New Customers Acquired in June 2023

## Business Problem

The marketing team ran a campaign in June 2023 and wants to analyze the number of new customers who signed up during that period.

## Fields to Retrieve

The query retrieves the following details for customers who signed up in June 2023:

- `PARTY_ID`
- `FIRST_NAME`
- `LAST_NAME`
- `EMAIL`
- `PHONE`
- `ENTRY_DATE`

## SQL Query

```sql
SELECT
    PT.PARTY_ID,
    PER.FIRST_NAME,
    PER.LAST_NAME,
    PT.CREATED_DATE AS ENTRY_DATE,
    CM.INFO_STRING AS EMAIL,
    TN.CONTACT_NUMBER AS PHONE,
    PR.ROLE_TYPE_ID AS ROLE
FROM PARTY PT
JOIN PERSON PER ON PT.PARTY_ID = PER.PARTY_ID
JOIN PARTY_ROLE PR ON PT.PARTY_ID = PR.PARTY_ID
JOIN PARTY_CONTACT_MECH PCM ON PT.PARTY_ID = PCM.PARTY_ID
JOIN CONTACT_MECH CM ON PCM.CONTACT_MECH_ID = CM.CONTACT_MECH_ID
JOIN TELECOM_NUMBER TN ON CM.CONTACT_MECH_ID = TN.CONTACT_MECH_ID
WHERE PR.ROLE_TYPE_ID = 'CUSTOMER'
AND PT.CREATED_DATE BETWEEN '2023-06-01' AND '2023-06-30';
```

## Query Explanation

To retrieve the list of new customers who signed up in June 2023:

1. **Join `PARTY` and `PERSON`**: Retrieves basic customer details.
2. **Filter by `CREATED_DATE`**: Ensures only customers created within June 2023 are included.
3. **Join `PARTY_ROLE`**: Filters to only include entities with a `CUSTOMER` role.
4. **Join `PARTY_CONTACT_MECH` and `CONTACT_MECH`**: Fetches the email addresses.
5. **Join `TELECOM_NUMBER`**: Retrieves the phone number of each customer.

## Query Cost

- Estimated query cost: **17,319**  
- Expected rows retrieved: **7,000**
