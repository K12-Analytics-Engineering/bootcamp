# Dimensional Modeling

> Dimensional modeling is a design approach optimized for analytic systems. A dimensional model captures how a process is measured. Data elements that represent measurements are called facts. Data elements that provide context for measurements are called dimensions. These elements are grouped into dimension tables and fact tables. Implemented in a relational database, the design is called a star schema.
>
> -- <cite>Christopher Adamson: <ins>[Star Schema The Complete Reference](https://www.amazon.com/Schema-Complete-Reference-Christopher-Adamson/dp/0071744320)</ins></cite>


[*Operational and analytical data systems*](./operational_and_analytical_data_systems.md) walks through why it is essential to have a separate data system specific to analytics. Analytic data models look very different than the transactional model that powers the Ed-Fi ODS. Analytic data models consist of dimension and fact tables, and the Ed-Fi Alliance provides us with those via the [Analytics Middle Tier](https://techdocs.ed-fi.org/display/EDFITOOLS/Analytics+Middle+Tier) (AMT). AMT consists of fact tables that measure student attendance, grades, assessments, and more. Attendance tables in the Ed-Fi ODS store student attendance in an operational context meant to support transactional processing. AMT's attendance fact table stores student attendance in the context of analytics where attendance is being measured. The fact tables can be joined onto dimensions that describe students, staff, parents, sections, and more.

While the Analytics Middle Tier tooling released by the Ed-Fi Alliance creates a set of database views on top of the ODS, it is better idea to extract data from the Ed-Fi API to create the AMT dimension and fact tables in a cloud data warehouse that is specifically meant for analytics type SQL queries. This [GitHub repo](https://github.com/K12-Analytics-Engineering/dagster-edfi-api-to-bq-amt) has a production ready [Dagster](https://dagster.io/) job to do just that.

The Analytics Middle Tier follows a star schema design. Star schema was invented at a time when we did not have columnar cloud data warehouses and storage was expensive. This led to a design that denormalizes data from transactional systems, but organizes data in such a way that reduces duplication to keep storage low. Fact tables are typically narrow and long while dimension tables are wide and shorter. A student's name is store in the student dimension and joined to a fact table when that information is needed.

Today storage is cheaper and we have data warehouse products such as BigQuery that perform very well with wide tables. We also have [dbt](https://www.getdbt.com/) which gives us a way to organize our data models so we can store a piece of data such as a student's name in many places, but track the lineage. Inside the Dagster repo above are dbt models (ie. [`stg_student_assessment_fact`](https://github.com/K12-Analytics-Engineering/dagster-edfi-api-to-bq-amt/blob/master/project_dbt/models/staging/stg_student_assessment_fact.sql)) that "pre-join" fact tables to various dimensions and utilize BigQuery's nested and repeated fields to provide staging versions of base AMT tables that can be used in BI tools more effectively.




### Resources that informed this page:
* [book] Christopher Adamson: <ins>[Star Schema The Complete Reference](https://www.amazon.com/Schema-Complete-Reference-Christopher-Adamson/dp/0071744320)</ins>
* [book] Ralph Kimball: <ins>[The Data Warehouse Toolkit](https://www.amazon.com/Data-Warehouse-Toolkit-Definitive-Dimensional/dp/1118530802)</ins>
* [youtube] [Kimball in the context of the modern data warehouse: what's worth keeping, and what's not](https://youtu.be/3OcS2TMXELU)
