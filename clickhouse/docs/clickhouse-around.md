curl https://clickhouse.com/ | sh

## Learn
https://learn.clickhouse.com/learner_module/show/1328489?lesson_id=7667283&section_id=75703125


./clickhouse server

./clickhouse client


Real time analytics engine

table engine - determines how data is stored in clickhouse

granule - is smallest unit thas is loaded into memory and referenced by primary keys,
each primary key is pointing to granules

part - is folder on disk created each to client run inserts,
   it contains files with values per column, and and index file

primary key index is kept in memory for efficient queryies 