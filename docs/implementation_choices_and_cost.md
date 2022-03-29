# Implementation choices and cost

![Data stack](/assets/k12_open_source_data_stack.png)

## Implementation costs

While the various components above (Ed-Fi, Dagster, dbt, and Superset) can be deployed on-prem or in any of the major cloud providers, the tooling in this GitHub organization will focus on Google Cloud Platform (GCP). This is largely due to the generous free tier of various products such as Google BigQuery. The data stack itself will highlight [Apache Superset](https://superset.apache.org) as a great open source data visualization platform, but it should also be noted that BigQuery and [Google Data Studio](https://datastudio.google.com) pairing very well together.


| Component             | Google Cloud product | Configuration                                   | Yearly cost            | Committed usage cost                     |
| --------------------- | -------------------- | ----------------------------------------------- | ---------------------- | ---------------------------------------- |
| Ed-Fi ODS             | Cloud SQL            | PostgreSQL 11,<br>2 vCPUs,<br>6 GB of memory      | $750 / year              | 1 year: $568 / year<br />3 year: $370 / year |
| Ed-Fi API             | Cloud Run            | 2 vCPUs,<br>2 GB of memory,<br>3 max instances    | Free<br>*Free tier is 2 million<br>requests per month* |          |
| Ed-Fi Admin App       | Cloud Run            | 2 vCPUs,<br>1 GB of memory,<br>1 max instance     | Free<br>*Free tier is 2 million<br>requests per month* |          |
| Dagster               | Compute Engine VM    | Preemptible VM,<br>2 vCPUs,<br>3.5 GB of memory   | $100 / year                       | N/A |
| Dagster               | Cloud SQL            | PostgreSQL 11,<br>Shared CPU,<br>0.6 GB of memory | $120 / year                       | N/A |
| In-memory analysis service | BI Query Engine | 1 GB of capacity                           | Free<br>*Free tier is first GB of capacity.<br>$360/year for each additional GB* | |
