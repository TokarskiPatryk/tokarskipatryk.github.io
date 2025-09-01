**TL;DR**: We replaced a complex transformation pipeline in Snowflake that used dynamically created SQL statements to move and deduplicate data from S3 with dynamic tables—one for each object. This approach eliminated the need for complicated pipelines and technical maintenance tables.

## Why This Matters

Managing streaming data pipelines in Snowflake often requires maintaining multiple custom procedures and tasks. When dealing with multiple data sources, deduplication requirements, and scheduling dependencies, teams typically need to handle:

- Incremental data processing requirements
    
- Complex SQL procedures that dynamically generate merge statements
    
- Debugging pipeline failures across interconnected tasks
    
- Scaling processing as data volume grows
    

This was the situation we faced before implementing Snowflake's dynamic tables for our data pipeline.

Thanks for reading Data Engineering Toolkit! Subscribe for free to receive new posts and support my work.

## What are Dynamic Tables in Snowflake?

[Dynamic tables](https://docs.snowflake.com/en/user-guide/dynamic-tables-about) in Snowflake are tables that refresh automatically on a defined schedule, moving and transforming data from specified sources. They can take one or more tables in the transformation script and can look only for changes in source tables, incrementally moving data which speeds up the process when dealing with large tables.

![Visual representation of automated refresh process between base objects and dynamic tables](../assets/dynamic_tables_sf.webp)

Source: [https://docs.snowflake.com/en/user-guide/dynamic-tables-about](https://docs.snowflake.com/en/user-guide/dynamic-tables-about)

> 💡 **Note**: Dynamic tables handle incremental processing automatically. You don't need to write additional logic to detect new records - Snowflake manages this functionality internally.

Without dynamic tables, we would need to create target tables ourselves, define procedures containing transformations, and create tasks that execute these procedures on a schedule. If we additionally wanted to transfer only data that was created since the last operation in our custom solution, we would need to create appropriate logic responsible for detecting new records. This was exactly the architecture we had initially in our Snowflake database.

## Previous Architecture (Pipeline of Tasks and Procedures)

In our old architecture, we used procedures and tasks chained together in a pipeline to transform streamed data from S3. These procedures dynamically created code to merge selected subsets of queries (from the previous successful timestamp of a given table transformation up to the execution time of the task) for every table that needed to be transformed. Meanwhile, data was deduplicated: some records were modified with new values, some were added, and some were marked as retired.


[Example pipeline of procedures and tasks used to ETL streaming data.](../assets/dynamic_tables_pipeline.webp)


We also needed to implement parallel processing of tables because the default solution processed them one by one with dynamic SQL, which made the process longer. Implementing parallel transformation procedures sped up the process but further complicated maintenance.

After researching dynamic tables, we decided to evaluate them as an alternative solution.

## Current Architecture (Dynamic Tables)

The current architecture doesn't contain any pipeline because all dynamic tables run independently on a given schedule. There's also no need to maintain any additional procedures and tasks, because all the code for implementing dynamic tables, including transformations and scheduling, is contained in their definition. This has reduced the overall complexity and simplified future maintenance of the solution.

Here's an example of how we define a dynamic table for deduplicating streaming events:

```sql
CREATE OR REPLACE DYNAMIC TABLE user_events_deduped
TARGET_LAG = '15 minutes'
WAREHOUSE = compute_wh
AS
SELECT
    user_id,
    event_type,
    event_timestamp,
    latest_data
FROM raw_events
QUALIFY ROW_NUMBER() OVER (
    PARTITION BY user_id, event_type
    ORDER BY event_timestamp DESC
) = 1;
```

This single definition replaces what used to be multiple procedures, merge statements, and task dependencies. The `TARGET_LAG` parameter ensures data freshness while `QUALIFY` handles our deduplication logic.

## Trade-offs to Consider

## Limited Logging Capabilities

We lost the detailed log tracking we had in the original architecture, which told us whether errors occurred and for which tables. Every execution and procedural errors were logged in our custom solution. With dynamic tables, there's no such granular logging because Snowflake's implementation automatically detects differences in data and performs operations at specified intervals.

## SQL Transformation Limitations

There are several limitations on what types of transformations you can perform in dynamic tables. In our case, these weren't significant constraints since we were deduplicating data from one source table. However, when using multiple source tables and more complex transformations, these limitations could be more important.

Key limitations include:

- No support for external functions or stored procedures
    
- Limitations in using CURRENT_TIMESTAMP inside SELECT
    
- No access history tracking for auditing purposes
    

It is worth mentioning that there are different technical limitations for incremental refresh and full refresh. For detailed information, see the documentation on [supported queries](https://docs.snowflake.com/en/user-guide/dynamic-tables-supported-queries) and [limitations](https://docs.snowflake.com/en/user-guide/dynamic-tables-limitations).

## Performance

If there's interest, I can describe a performance comparison between both solutions on datasets in the future. Our initial observations show improved resource utilization and reduced maintenance overhead, but a detailed analysis would provide more interesting metrics.