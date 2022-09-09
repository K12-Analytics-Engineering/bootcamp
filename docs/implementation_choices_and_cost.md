# Implementation choices and cost

![Data stack](/assets/k12_data_stack.png)

## Implementation costs

While the various components above (Ed-Fi, Dagster, and dbt) can be deployed on-prem or in any of the major cloud providers, the tooling in this GitHub organization focuses on Google Cloud Platform (GCP). This is largely due to the generous free tier of various products (Google Cloud Run and BigQuery).


| Component             | Google Cloud product | Configuration                                   | Yearly cost            | Committed usage cost                     |
| --------------------- | -------------------- | ----------------------------------------------- | ---------------------- | ---------------------------------------- |
| Ed-Fi ODS             | Cloud SQL            | PostgreSQL 11,<br>1 vCPU,<br>6 GB of memory      | $750 / year              | 1 year: $568 / year<br />3 year: $370 / year |
| Ed-Fi API             | Cloud Run            | 2 vCPUs,<br>2 GB of memory,<br>3 max instances    | Free<br>*Free tier is 2 million<br>requests per month* |          |
| Ed-Fi Admin App       | Cloud Run            | 2 vCPUs,<br>1 GB of memory,<br>1 max instance     | Free<br>*Free tier is 2 million<br>requests per month* |          |
| Dagster               | Google Kubernetes Engine | GKE Autopilot cluster   | $250 / year                       | N/A |
| Dagster               | Cloud SQL            | PostgreSQL 11,<br>Shared CPU,<br>0.6 GB of memory | $120 / year                       | N/A |
| Data warehouse        | BigQuery             |                                                   | Free<br>*Free tier is first  10GB of storage and first 1 TB of query processing* | |
| In-memory analysis service | BI Query Engine | 1 GB of capacity                                  | Free<br>*Free tier is first GB of capacity.<br>$360/year for each additional GB* | |
