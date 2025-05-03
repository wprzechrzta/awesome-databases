guardrails

# Around multi-tenancy in ClickHouse

This approach is useful if each tenant requires a large number of tables and possibly 
materialized views, and has different data schema. However, it may become challenging to manage if the number of tenants is large.


- separate db: https://github.com/ClickHouse/clickhouse-docs/blob/main/docs/cloud/bestpractices/multitenancy.md

- separate service: https://github.com/ClickHouse/clickhouse-docs/blob/main/docs/cloud/bestpractices/multitenancy.md#separate-cloud-service-separate-service
  The most radical approach is to use a different ClickHouse service per tenant.

This less common method would be a solution if tenants data are required to be stored in different regions 
- for legal, security or proximity reasons.
each requires their own infrastructure to run

- best practices https://clickhouse.com/docs/cloud/bestpractices
  Services per organization: 20 (soft)
  Services per warehouse: 5 (soft)


## Tiers https://clickhouse.com/docs/cloud/manage/api/services-api-reference
DEPRECATED for BASIC, SCALE and ENTERPRISE organization tiers. 
Tier of the service: 'development', 'production', 'dedicated_high_mem', 
'dedicated_high_cpu', 'dedicated_standard', 'dedicated_standard_n2d_standard_4', 
'dedicated_standard_n2d_standard_8', 'dedicated_standard_n2d_standard_32', 'dedicated_standard_n2d_standard_128', 'dedicated_standard_n2d_standard_32_16SSD', 'dedicated_standard_n2d_standard_64_24SSD'. 
Production services scale, Development are fixed size.
Azure services don't support Development tier


## Api to update service
It is possible to manage the service using the API.
https://clickhouse.com/docs/cloud/manage/api/services-api-reference#update-service-auto-scaling-settings-1
https://clickhouse.com/docs/cloud/manage/api/services-api-reference#update-service-auto-scaling-settings

## Cost API
https://clickhouse.com/docs/cloud/manage/api/usageCost-api-reference