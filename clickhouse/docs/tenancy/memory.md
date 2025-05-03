
## Server settings
https://clickhouse.com/docs/operations/server-configuration-parameters/settings
max_server_memory_usage
max_server_memory_usage_to_ram_ratio
max_memory_usage_for_user - The maximum amount of RAM to use for running a user’s queries on a single server.

- nice page about memory settings: https://chistadata.com/knowledge-base/clickhouse-memory-configuration/

```shell  see the current memory consumption for each query
SHOW PROCESSLIST
```
SET max_memory_usage = 8000000000; # 8GB

max_memory_usage - limit for single query on single server
max_memory_usage
max_concurrent_queries
max_concurrent_insert_queries
max_concurrent_select_queries
max_concurrent_queries_for_user
max_concurrent_queries_for_all_users
max_memory_usage_for_user

- example allocations
  https://chistadata.com/knowledge-base/chistadata-cloud/

- github memory settings: https://github.com/ClickHouse/ClickHouse/blob/e5b96bd93b53d2c1130a249769be1049141ef386/programs/server/config.xml#L239-L250