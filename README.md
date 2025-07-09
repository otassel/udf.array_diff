# udf.array_diff
BigQuery UDF to return items from the first array that are not in the second one

```sql
CREATE OR REPLACE FUNCTION `altancy.udf.array_diff`(array1 ANY TYPE, array2 ANY TYPE)
AS (
    (
        SELECT ARRAY_AGG(val)
        FROM UNNEST(array1) AS val
        WHERE val NOT IN UNNEST(array2)
        HAVING COUNT(val) > 0
    )
);
```
