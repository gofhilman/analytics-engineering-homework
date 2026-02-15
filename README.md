# analytics-engineering-homework

Homework solution for Analytics Engineering

Problems: <https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2026/04-analytics-engineering/homework.md>

1. If you run `dbt run --select int_trips_unioned`, the model that will be built is `int_trips_unioned` only.

2. If you run `dbt test --select fct_trips`, dbt will fail the test, returning a non-zero exit code.

3. 12,184

4. East Harlem North

    ```sql
    SELECT 
        pickup_zone,
        SUM(revenue_monthly_total_amount) AS total_revenue_2020
    FROM `even-lyceum-282418.analytics_engineering.fct_monthly_zone_revenue`
    WHERE service_type = 'Green'
        AND EXTRACT(YEAR FROM revenue_month) = 2020
    GROUP BY pickup_zone
    ORDER BY total_revenue_2020 DESC
    LIMIT 1;
    ```

5. 384,624

    ```sql
    SELECT 
        SUM(total_monthly_trips) AS total_trips_october_2019
    FROM `even-lyceum-282418.analytics_engineering.fct_monthly_zone_revenue`
    WHERE service_type = 'Green'
        AND revenue_month = DATE '2019-10-01';
    ```

6. 43,244,693

    ```sql
    SELECT 
        COUNT(*) FROM `even-lyceum-282418.analytics_engineering.stg_fhv_tripdata`;
    ```
