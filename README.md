# analytics-engineering-homework

Homework solution for Analytics Engineering

Problems: <https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2026/04-analytics-engineering/homework.md>

1. If you run `dbt run --select int_trips_unioned`, the model that will be built is `int_trips_unioned` only.

    To prepare the data, set up kestra using `docker-compose.yaml` by providing the Google Cloud Platform service account secrets in `.env_encoded`. Then upload and run kestra flow `kestra-flows/01-gcp-kv.yaml`, `kestra-flows/02-gcp-setup.yaml`, `kestra-flows/03-gcp-taxi.yaml`, `kestra-flows/04-gcp-loop-taxi.yaml`, and `kestra-flows/05-gcp-taxi-tables.yaml` simultaneously by using required data for the problems. Then, execute `dbt build --target prod`in `analytics_engineering` directory.

2. If you run `dbt test --select fct_trips`, dbt will fail the test, returning a non-zero exit code.

3. The count of records in the `fct_monthly_zone_revenue` model is 12,184.

    ```sql
    SELECT 
        COUNT(*) FROM `even-lyceum-282418.analytics_engineering.fct_monthly_zone_revenue`;
    ```

4. The pickup zone with the highest total revenue (`revenue_monthly_total_amount`) for `Green` taxi trips in 2020 is East Harlem North.

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

5. The total number of trips (`total_monthly_trips`) for `Green` taxis in October 2019 is 384,624.

    ```sql
    SELECT 
        SUM(total_monthly_trips) AS total_trips_october_2019
    FROM `even-lyceum-282418.analytics_engineering.fct_monthly_zone_revenue`
    WHERE service_type = 'Green'
        AND revenue_month = DATE '2019-10-01';
    ```

6. The count of records in `stg_fhv_tripdata` is 43,244,693.

    ```sql
    SELECT 
        COUNT(*) FROM `even-lyceum-282418.analytics_engineering.stg_fhv_tripdata`;
    ```
