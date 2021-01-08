´´´
--- using temp array
WITH TEMP AS (
SELECT name, 
carr.id AS car_id, 
carr.model AS car_model, 
man.year AS manufacture_year,
purchase
FROM burak_intisah.semi_structured_hw
CROSS JOIN unnest(manufacture) AS man 
CROSS JOIN unnest(car) AS carr
ON carr.id = man.id 
)
SELECT name, car_id, car_model, manufacture_year, 
ARRAY (SELECT AS STRUCT p.id, timestamp_add(date,interval 3 hour) AS date FROM unnest(purchase) AS p) AS purchase 
FROM TEMP
´´´
