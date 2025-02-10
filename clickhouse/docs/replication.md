## About replication

https://clickhouse.com/docs/en/engines/table-engines/mergetree-family/replication

important: add to server config file:
<default_replica_path>/clickhouse/tables/{shard}/{database}/{table}</default_replica_path>
<default_replica_name>{replica}</default_replica_name>

```bash
ENGINE = ReplicatedMergeTree(
    '/clickhouse/tables/{shard}/table_name',
    '{replica}',
    ver
)
```

CREATE TABLE table_name ( ... ) ENGINE = ReplicatedMergeTree('zookeeper_name_configured_in_auxiliary_zookeepers:path', 'replica_name') ...

- using macros in table definition
parameters in DDL are taken from macros
```sql
CREATE TABLE table_name
(
    EventDate DateTime,
    CounterID UInt32,
    UserID UInt32,
    ver UInt16
ENGINE = ReplicatedReplacingMergeTree('/clickhouse/tables/{layer}-{shard}/table_name', '{replica}', ver)
PARTITION BY toYYYYMM(EventDate)
ORDER BY (CounterID, EventDate, intHash32(UserID))
SAMPLE BY intHash32(UserID);
```

```xml
<macros>
    <shard>02</shard>
    <replica>example05-02-1</replica>
</macros> 
```


-- After configuring defaults:

<default_replica_path>/clickhouse/tables/{shard}/{database}/{table}</default_replica_path>
<default_replica_name>{replica}</default_replica_name>

```sql
CREATE TABLE table_name (
	x UInt32
) ENGINE = ReplicatedMergeTree
ORDER BY x;
```
is same as 
```sql
CREATE TABLE table_name (
	x UInt32
) ENGINE = ReplicatedMergeTree('/clickhouse/tables/{shard}/{database}/table_name', '{replica}')
ORDER BY x;
```