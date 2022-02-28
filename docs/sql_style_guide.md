# SQL Style Guide

## Field Naming and Reference Conventions

* Field names should use snake case
* An id, name, or generally ambiguous value such as type should always be prefixed by what it is identifying or naming
* Field names should reflect the Ed-Fi Data Standard when possible

```sql

  -- good
  SELECT
    id          AS student_unique_id,
    lname       AS student_last_surname,
    firstname   AS student_first_name,
    ...

  -- bad
  SELECT
    id,
    lname,
    firstname,
    ...

```

* When joining tables and referencing columns from both, strongly prefer to reference the full table name instead of an alias. When the table name is long (~30), try to rename the CTE if possible, and lastly consider aliasing to something descriptive.

```sql

-- good
SELECT    
    dim_student.student_unique_id,
    dim_section.course_title,
    fct_student_section_grade.numeric_grade_earned,
    fct_student_section_grade.letter_grade_earned
FROM fct_student_section_grade
LEFT JOIN dim_section
    ON fct_student_section_grade.section_key = dim_section.section_key
LEFT JOIN dim_student
    ON fct_student_section_grade.student_key = dim_student.student_key


-- bad
SELECT    
    c.student_unique_id,
    b.course_title,
    a.numeric_grade_earned,
    a.letter_grade_earned
FROM fct_student_section_grade a
LEFT JOIN dim_section b
    ON a.section_key = b.section_key
LEFT JOIN dim_student c
    ON a.student_key = c.student_key

```

* Boolean field names should start with `has`, `is`, or `does`

```sql

  -- good
  SELECT
    deleted AS is_deleted,
    sla     AS has_sla
  FROM table

  -- bad
  SELECT
    deleted,
    sla
  FROM table

  ```


## Use CTEs (Common Table Expressions), not subqueries

* [CTEs make SQL more readable and are more performant](https://www.alisa-in.tech/post/2019-10-02-ctes/)
* CTEs should be placed at the top of the query
* Where performance permits, CTEs should perform a single, logical unit of work
* CTE names should be as concise as possible while still being clear
* Avoid long names like `replace_account_id_with_master_record_id` and prefer a shorter name with a comment in the CTE. This will help avoid table aliasing in joins
* CTEs with confusing or notable logic should be commented in file and documented in Dataform docs
* CTEs that are duplicated across models should be pulled out into their own models
* Leave an empty row above and below the query statement

## Functions
Consider simplifying a repetitive CASE statement where possible:

```sql

-- ok
CASE
    WHEN field_id = 1 THEN 'date'
    WHEN field_id = 2 THEN 'integer'
    WHEN field_id = 3 THEN 'currency'
    WHEN field_id = 4 THEN 'boolean'
    WHEN field_id = 5 THEN 'variant'
    WHEN field_id = 6 THEN 'text'
END AS field_type

-- better
CASE field_id
    WHEN 1 THEN 'date'
    WHEN 2 THEN 'integer'
    WHEN 3 THEN 'currency'
    WHEN 4 THEN 'boolean'
    WHEN 5 THEN 'variant'
    WHEN 6 THEN 'text'
END AS field_type

```


# JOINs

* Be explicit when joining, e.g. use LEFT JOIN instead of JOIN
* Specify the order of a join with the FROM table first and JOIN table second:

```sql

-- good
FROM source
LEFT JOIN other_source
  ON source.id = other_source.id
WHERE ...

-- bad
FROM source
LEFT JOIN other_source
  ON other_source.id = source.id
WHERE ...

```


## General
* Within a CTE, the entire SQL statement should be indented 4 spaces

```sql

-- good
WITH my_data AS (

    SELECT *
    FROM all_data
    WHERE Filter = 'my_filter'

)

-- bad
WITH my_data  AS (

  SELECT *
  FROM all_data
  WHERE Filter = 'my_filter'

)

```

* Indentation within a query (e.g. columns, JOIN clauses, multi-line GROUP BY, etc.) should be indented 2 spaces
* Lines of SQL should be no longer than 80 characters
* Commas should be at the end-of-line (EOL) as a right comma
* When SELECTing, always give each column its own row, with the exception of SELECT * which can be on a single row
* DISTINCT should be included on the same row as SELECT
* When aliasing use AS, strive to align the original column names on a single vertical line and the AS keyword on a separate vertical line
* Prefer UNION ALL to UNION. This is because a UNION could indicate upstream data integrity issue that are better solved elsewhere
* Prefer != to <>. This is because != is more common in other programming languages and reads like "not equal" which is how we're more likely to speak
* DO NOT OPTIMIZE FOR A SMALLER NUMBER OF LINES OF CODE. NEWLINES ARE CHEAP. BRAIN TIME IS EXPENSIVE.



## Resources that informed this page:
* [GitLab’s SQL style guide](https://about.gitlab.com/handbook/business-technology/data-team/platform/sql-style-guide/)
* [dbt Labs' style guide](https://github.com/dbt-labs/corp/blob/master/dbt_style_guide.md)
