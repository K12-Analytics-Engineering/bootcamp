# K12 open source data stack

The material in this repository aims to build an understanding around the architecture shown below. The articles will try to explain the *why* behind the various components of the K12 open source data stack. The other repositories that contain the actual code to implement will be far more tactical and will explain the *how* behind implementing.

![Data stack](/assets/k12_open_source_data_stack.png)

## Implementation costs

While the various components above (Ed-Fi, Dagster, dbt, and Superset) can be deployed on-prem or in any of the major cloud providers, the tooling in this GitHub organization will focus on Google Cloud Platform. This is largely due to the generous free tier of various products such as Google BigQuery. Google Cloud Platform is also the focus due to BigQuery and [Google Data Studio](https://datastudio.google.com) pairing very well together. The data stack itself will highlight [Apache Superset](https://superset.apache.org) as a great open source data visualization platform, but will also weigh it against Google Data Studio which is quickly gaining a foothold in education.

| Data Stack Component  | Google Cloud Product | Configuration     | Yearly Cost     |
| --------------------- | -------------------- | ----------------- | --------------- |
| Ed-Fi ODS             | Cloud SQL            |            |                   |
| Ed-Fi API             | Cloud Run            |            |                   |
| Ed-Fi Admin App       | Cloud Run            |            |                   |
| Dagster               | Dagster Cloud + Compute Engine VM            |            |                   |
