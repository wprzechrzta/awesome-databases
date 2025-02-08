
show databases;
show tables;
show tables in default;

see: https://clickhouse.com/docs/en/interfaces/cli
clickhouse-client -h localhost:9000

## Create table

CREATE TABLE my_first_table
(
user_id UInt32,
message String,
timestamp DateTime,
metric Float32
)
ENGINE = MergeTree
PRIMARY KEY (user_id, timestamp)

    
## Insert batch
INSERT INTO my_first_table (user_id, message, timestamp, metric) VALUES
(101, 'Hello, ClickHouse!',                                 now(),       -1.0    ),
(102, 'Insert a lot of rows per batch',                     yesterday(), 1.41421 ),
(102, 'Sort your data based on your commonly-used queries', today(),     2.718   ),
(101, 'Granules are the smallest chunks of data read',      now() + 5,   3.14159 )

## Select 
SELECT *
FROM my_first_table
ORDER BY timestamp



### Example with s3 
SELECT
passenger_count,
avg(toFloat32(total_amount))
FROM s3(
'https://datasets-documentation.s3.eu-west-3.amazonaws.com/nyc-taxi/trips_0.gz',
'TabSeparatedWithNames'
)
GROUP BY passenger_count
ORDER BY passenger_count;

## USing file
- put file into user_files/ dir

DESCRIBE TABLE file('trips.tsv')

SELECT count()
FROM file(
'trips.tsv',
'TabSeparatedWithNames'
)

SELECT
pickup_date,
pickup_ntaname,
SUM(1) AS number_of_trips
FROM trips
GROUP BY pickup_date, pickup_ntaname
ORDER BY pickup_date ASC

## Experiment with pypi_python dataset
SELECT PROJECT
count() as c
FROM s3()
GROUP BY PROJECT
ORDER BY c DESC;


SELECT
  toStartOfMonth(TIMESTAMP) as month,
  PROJECT,
  count()
FROM s3(...)
GROUP BY month, PROJECT
ORDER BY 3 DESC;

## UK price paid
https://clickhouse.com/docs/en/getting-started/example-datasets/uk-price-paid

SELECT formatReadableQuantity(count())
FROM uk_price_paid;

SELECT * from uk_price_paid
LIMIT 100;

SELECT avg(PRICE) from uk_price_paid;

SELECT 
  avg(price),
  count();
  town
FROM uk_price_paid
GROUP BY town
ORDER BY 1 DESC;

