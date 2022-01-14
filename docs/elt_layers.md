# ELT and data warehouse layers

In an ELT workflow, transformations happen in the data warehouse layer via SQL. Those transformations are typically managed in a tool such as [dbt](https://www.getdbt.com). Data models are created that reference source data and those data models can be referenced by other data models. Seeing these transformations as different layers of your warehouse will help ensure your data models are well understood and utilized. Without a way to organize your warehouse layer, you risk ending up with an environment that feels like that drawer we all have in our house full of random shit.

## Sources
These are the tables where the raw data first lands from your source operational systems. The tables here have a schema that is defined by the source system. In an environment that follows what is shown in [*Operational and analytical data systems*](./operational_and_analytical_data_systems.md), these tables are sourced from the Ed-Fi API. If you are extracting data from an operational system and loading it directly into your warehouse without sending it to your Ed-Fi API first to be mapped to the Ed-Fi Data Standard and validated, the tables will have a schema that is defined by the vendor's API, SFTP drop, or other method of delivery.

## Staging
Each data model here matches 1:1 with a table in your source layer. This is your place to cast columns to a more appropriate data type or if the data is not sourced from the Ed-Fi API, this is your place to rename columns to align with the Ed-Fi Data Standard. If the source table came from the Ed-Fi API, you may not need a staging data model for it. However, if it did not, you'll likely always need one.

## Dimension and fact tables
As the [*Dimensional modeling*](./dimensional_modeling.md) article explains, star schema was created before we had powerful, columnar cloud data warehouses such as BigQuery and Snowflake. However, the design process that dimensional modeling necessitates is helpful in the sense that it allows us to think about our data in the context of dimensions and facts. Is a specific piece of data contextual (ie. gender, race, etc.) or is it measuring something (ie. grades, attendance, etc).

Organizing data from the upstream layers into dimension and fact tables also allows you to combine disparate sources. Data from your Ed-Fi API may have iReady assessment data, and you may have a separate extract and load job to move Performance Matters assessment data into your warehouse bypassing the Ed-Fi API. In this layer you may create a student assessment fact table that includes data from both sources.

## Make it wide
I typically find it helpful to create a `stg_` version of all of my fact tables that join on all dimensions so I have one big, wide table. Some cloud data warehouse products such as BigQuery have support for nested data (in BigQuery these are referred to as nested and repeated fields). I utilize nested data if joins onto dimensions are going to duplicate the data found in the fact table.


## Resources that informed this page:
* [blog] [How we structure our dbt projects](https://discourse.getdbt.com/t/how-we-structure-our-dbt-projects/355)
