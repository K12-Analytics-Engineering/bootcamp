# Data marts documentation

The [Ed-Fi API ➡ Analytics Middle Tier repo](https://github.com/K12-Analytics-Engineering/dagster-edfi-api-to-bq-amt) pulls data from the Ed-Fi API to create data marts in BigQuery for use in analytics. It also sets the analytics engineer up to continue to build additional data models and metrics on top of that through the use of [dbt](https://www.getdbt.com). The dbt models that are included with the repo already do this a little bit to create things like a student dim that is not in Ed-Fi's Analytics Middle Tier. This documentation should serve as a companion guide to Ed-Fi's [official documentation](https://techdocs.ed-fi.org/display/EDFITOOLS/AMT+User+Guide) as well as go into depth with respect to the additions that we made with this implementation of the Ed-Fi spec.

| Collection      | Name                       |
| --------------- | -------------------------- |
| Core            | [Dim Date](#dim_date)      |

------------------------------------------------------------------

## Dim Date
A date dimension table can be found in almost every dimensional model and allows the analytics engineer to look at student performance across different time periods. An explicit date dimension table can also help store date attributes that are not supported by a SQL date function (ie. month sort order in the context of a school year).

This dimension table notably lacks the date key found in Ed-Fi's Analytics Middle Tier. This is also counter to what Kimball tells us to do. Instead, fact tables found in the marts that include a date, use the DATE type. Kimball argues that if a fact table does this, it will cause folks to use SQL functions on that date to extract items like month name and avoid the join to the date dimension when they need to retrieve such information. You should use the date if you need the date and join on the date dimension if you need more.

| Column Name            | Data Type          | Description         | Example           |
| ---------------------- | ------------------ | ------------------- | ----------------- |
| date                   | DATE               | Calendar date       | 2022-01-24        |
| day                    | INTEGER            | Day number          | 24                |
| month                  | STRING             | Month number        | 1                 |
| month_name             | STRING             | Month name          | January           |
| calendar_quarter       | INTEGER            | Based on 1: Jan-Mar, 2: Apr-Jun, 3: Jul-Sep, 4: Oct-Dec                    | 1        |
| calendar_quarter_name  | STRING             | Calendar quarter name  | First         |
| calendar_year          | STRING             | Calendar year       | 2022             |
| month_sort_order       | INTEGER            | Looks at school year as July - June    | 7        |


## Resources that informed this page:
* [Official Ed-Fi AMT documentation](https://techdocs.ed-fi.org/display/EDFITOOLS/AMT+User+Guide)
* [book] Ralph Kimball: <ins>[The Data Warehouse Toolkit](https://www.amazon.com/Data-Warehouse-Toolkit-Definitive-Dimensional/dp/1118530802)</ins>
