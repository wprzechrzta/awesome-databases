## Settings
https://clickhouse.com/docs/en/operations/settings/settings#default_table_engine

<default_table_engine> </default_table_engine>
### important: add to server config file: (standalone installation)
<default_replica_path>/clickhouse/tables/{shard}/{database}/{table}</default_replica_path>
<default_replica_name>{replica}</default_replica_name>



- find table engines
```sql
SET default_table_engine = 'Log';
SELECT name, value, changed FROM system.settings WHERE name = 'default_table_engine';
```

## About distributed
look into system.clusters
https://clickhouse.com/docs/en/engines/table-engines/special/distributed

Tables with Distributed engine do not store any data of their own, but allow distributed query processing on multiple servers. Reading is automatically parallelized.
During a read, the table indexes on remote servers are used, if there are any.

If you need to send a query to an unknown set of shards and replicas each time,
you do not need to create a Distributed table – use the remote table function instead.
See the section Table functions.

## Reading from distributed
When querying a Distributed table, SELECT queries are sent to all shards and work regardless of how
data is distributed across the shards (they can be distributed completely randomly).

```sql
CREATE TABLE hits_all AS hits
ENGINE = Distributed(logs, default, hits[, sharding_key[, policy_name]])
SETTINGS
    fsync_after_insert=0,
    fsync_directories=0;
```

currentDatabase()

## Allow distributed DDL
```xml

<remote_servers>
  <logs>
    <allow_distributed_ddl_queries>true</allow_distributed_ddl_queries>
```

# Reading which replica? https://clickhouse.com/docs/en/operations/settings/settings#load_balancing