


- check distributed table creation
```sql
-- Check if tables exist on all nodes
SELECT 
    hostName() AS host,
    database,
    name,
    engine
FROM clusterAllReplicas('cluster_3shards_2replicas', system.tables)
WHERE database = 'your_database'
ORDER BY host, name;
```

For synchronous writes, you can use the insert_distributed_sync=1 setting

-- check rows count accross shards
```sql
-- Check row counts across shards
SELECT 
    hostName() AS host,
    count() AS rows
FROM clusterAllReplicas('cluster_3shards_2replicas', currentDatabase(), example_table)
GROUP BY host
ORDER BY host;
```

- automatic ddl distribution
```xmo
 <clickhouse>
    <!-- ... existing configuration ... -->

    <!-- Add these settings for distributed tables -->
    <distributed_ddl>
        <path>/clickhouse/task_queue/ddl</path>
        <pool_size>1</pool_size>
        <cleanup_delay_period>60</cleanup_delay_period>
        <task_max_lifetime>600</task_max_lifetime>
    </distributed_ddl>
```