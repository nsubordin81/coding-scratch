# Section 1: Databricks Lakehouse Platform

## Describe the relationship between the data lakehouse and the data warehouse

**Your answer:**

data warehouse was a traditional way of running thigns in the past, it is useful especially for running large ETL jobs that output structured data. it is not as flexible for things like general purpose analytics with unstructured data, data exploration at scale that kind of thing. the data lake kind of has become a different architecture that allows data to be completely unstructured and is more flexible for doing work with data that doesn't require a structured output, but it lacks the governance and structure and controls and explicit schema of a data warehose. the data lakehose marries these two concepts with a metadata and governance layer that abstracts between all of the compute and the interactions so ML and analysis work from a customer lives alongside etl jobs and batch processign work and they both go through the same data quality checks but they can be flexible to support less structure in the data during and after processing.

## Identify the improvement in data quality in the data lakehouse over the data lake

**Your answer:**
the improvement would be the metadata and access layer. `note to self look this up and be able to articulate it better, you still haven't grokked it`

## Compare and contrast silver and gold tables, which workloads will use a bronze table as a source, which workloads will use a gold table as a source

**Your answer:**

## Identify elements of the Databricks Platform Architecture, such as what is located in the data plane versus the control plane and what resides in the customer’s cloud account

**Your answer:**
the 'data plane' is also I thinkt he compute plane which is what the customer's cloud account holds. it is actually the cloud resources that are providing the storage and the compute, they are managed and owned by the customer. this means that the vendor, databricks and amazon or azure or whoever, is already guaranteeing that the business sensitive data resides in an area totally managed byt he customer, and they have control and ownership for what they are working with. the control plan is where the batch and etl jobs, the cluster management, the notebooks, all of the things that I guess you would consider presentation are living. databricks manages that part, which is quite a bit to abstract away from the ucustomer, how spark and databricks interfaces interact with the cloud computer resources. the outputs are also on the compute plane so data only lives in the control plane as long as it needs to be stored in memory. `note you don't know exactly where the boundary is here`

## Differentiate between all-purpose clusters and jobs clusters

**Your answer:**
all purpose clusters are long running, they are meant to be for things like notebooks that live a while with the data, jobs that are shared by many users. they will have maybe less memory and compute power because they will be running and incurring cost longer, they are for data exploration and availability. job clusters are for things like bartch jobs and etls that run and then automatically stop and clean themselves up, they are configured for one, narrow job.

## Identify how cluster software is versioned using the Databricks Runtime

`not sure if I really have the answer to this one yet` what I do know is taht there are different types of runtimes that support different purposes for clusters. one ist he standard which is for most purposes. it contains prebuilt libraries for working with data in whatever of the supported langauges you want to work in. there is a scala version a spark version and an overall databricks version with each runtime. in addition to the standard flavor, there is the flavor for doing faster jobs, to accelerate the processing, this is called the photon processor. the next flavor after this is the ML flavor, and it supports machine learning with libraries pre installed like pytorch, tensorflow, and others like sklearn and scipy numpy and pandas. the runtimes make it so that you don't have to install a lot of packages when you work with a cluster, they are already there.

**Your answer:**

## Identify how clusters can be filtered to view those that are accessible by the user

**Your answer:**

## Describe how clusters are terminated and the impact of terminating a cluster

**Your answer:**

## Identify a scenario in which restarting the cluster will be useful

**Your answer:**

## Describe how to use multiple languages within the same notebook

**Your answer:**

## Identify how to run one notebook from within another notebook

**Your answer:**

## Identify how notebooks can be shared with others

**Your answer:**

## Describe how Databricks Repos enables CI/CD workflows in Databricks

**Your answer:**

## Identify Git operations available via Databricks Repos

**Your answer:**

## Identify limitations in Databricks Notebooks version control functionality relative to Repos

**Your answer:**

# Section 2: ELT with Apache Spark

## Extract data from a single file and from a directory of files

**Your answer:**

## Identify the prefix included after the FROM keyword as the data type

**Your answer:**

## Create a view, a temporary view, and a CTE as a reference to a file

**Your answer:**

## Identify that tables from external sources are not Delta Lake tables

**Your answer:**

## Create a table from a JDBC connection and from an external CSV file

**Your answer:**

## Identify how the count if function and the count where x is null can be used

**Your answer:**

## Identify how the count(row) skips NULL values

**Your answer:**

## Deduplicate rows from an existing Delta Lake table

**Your answer:**

## Create a new table from an existing table while removing duplicate rows

**Your answer:**

## Deduplicate a row based on specific columns

**Your answer:**

## Validate that the primary key is unique across all rows

**Your answer:**

## Validate that a field is associated with just one unique value in another field

**Your answer:**

## Validate that a value is not present in a specific field

**Your answer:**

## Cast a column to a timestamp

**Your answer:**

## Extract calendar data from a timestamp

**Your answer:**

## Extract a specific pattern from an existing string column

**Your answer:**

## Utilize the dot syntax to extract nested data fields

**Your answer:**

## Identify the benefits of using array functions

**Your answer:**

## Parse JSON strings into structs

**Your answer:**

## Identify which result will be returned based on a join query

**Your answer:**

## Identify a scenario to use the explode function versus the flatten function

**Your answer:**

## Identify the PIVOT clause as a way to convert data from a long format to a wide format

**Your answer:**

## Define a SQL UDF

**Your answer:**

## Identify the location of a function

**Your answer:**

## Describe the security model for sharing SQL UDFs

**Your answer:**

## Use CASE/WHEN in SQL code

**Your answer:**

## Leverage CASE/WHEN for custom control flow

**Your answer:**

# Section 3: Incremental Data Processing

## Identify where Delta Lake provides ACID transactions

**Your answer:**

## Identify the benefits of ACID transactions

**Your answer:**

## Identify whether a transaction is ACID-compliant

**Your answer:**

## Compare and contrast data and metadata

**Your answer:**

## Compare and contrast managed and external tables

**Your answer:**

## Identify a scenario to use an external table

**Your answer:**

## Create a managed table

**Your answer:**

## Identify the location of a table

**Your answer:**

## Inspect the directory structure of Delta Lake files

**Your answer:**

## Identify who has written previous versions of a table

**Your answer:**

## Review a history of table transactions

**Your answer:**

## Roll back a table to a previous version

**Your answer:**

## Identify that a table can be rolled back to a previous version

**Your answer:**

## Query a specific version of a table

**Your answer:**

## Identify why Zordering is beneficial to Delta Lake tables

**Your answer:**

## Identify how vacuum commits deletes

**Your answer:**

## Identify the kind of files Optimize compacts

**Your answer:**

## Identify CTAS as a solution

**Your answer:**

## Create a generated column

**Your answer:**

## Add a table comment

**Your answer:**

## Use CREATE OR REPLACE TABLE and INSERT OVERWRITE

**Your answer:**

## Compare and contrast CREATE OR REPLACE TABLE and INSERT OVERWRITE

**Your answer:**

## Identify a scenario in which MERGE should be used

**Your answer:**

## Identify MERGE as a command to deduplicate data upon writing

**Your answer:**

## Describe the benefits of the MERGE command

**Your answer:**

## Identify why a COPY INTO statement is not duplicating data in the target table

**Your answer:**

## Identify a scenario in which COPY INTO should be used

**Your answer:**

## Use COPY INTO to insert data

**Your answer:**

## Identify the components necessary to create a new DLT pipeline

**Your answer:**

## Identify the purpose of the target and of the notebook libraries in creating a pipeline

**Your answer:**

## Compare and contrast triggered and continuous pipelines in terms of cost and latency

**Your answer:**

## Identify which source location is utilizing Auto Loader

**Your answer:**

## Identify a scenario in which Auto Loader is beneficial

**Your answer:**

## Identify why Auto Loader has inferred all data to be STRING from a JSON source

**Your answer:**

## Identify the default behavior of a constraint violation

**Your answer:**

## Identify the impact of ON VIOLATION DROP ROW and ON VIOLATION FAIL UPDATE for a constraint violation

**Your answer:**

## Explain change data capture and the behavior of APPLY CHANGES INTO

**Your answer:**

## Query the events log to get metrics, perform audit logging, examine lineage

**Your answer:**

## Troubleshoot DLT syntax: Identify which notebook in a DLT pipeline produced an error, identify the need for LIVE in create statement, identify the need for STREAM in from clause

**Your answer:**

# Section 4: Production Pipelines

## Identify the benefits of using multiple tasks in Jobs

**Your answer:**

## Set up a predecessor task in Jobs

**Your answer:**

## Identify a scenario in which a predecessor task should be set up

**Your answer:**

## Review a task's execution history

**Your answer:**

## Identify CRON as a scheduling opportunity

**Your answer:**

## Debug a failed task

**Your answer:**

## Set up a retry policy in case of failure

**Your answer:**

## Create an alert in the case of a failed task

**Your answer:**

## Identify that an alert can be sent via email

**Your answer:**

# Section 5: Data Governance

## Identify one of the four areas of data governance

**Your answer:**

## Compare and contrast metastores and catalogs

**Your answer:**

## Identify Unity Catalog securables

**Your answer:**

## Define a service principal

**Your answer:**

## Identify the cluster security modes compatible with Unity Catalog

**Your answer:**

## Create a UC-enabled all-purpose cluster

**Your answer:**

## Create a DBSQL warehouse

**Your answer:**

## Identify how to query a three-layer namespace

**Your answer:**

## Implement data object access control

**Your answer:**

## Identify colocating metastores with a workspace as best practice

**Your answer:**

## Identify using service principals for connections as best practice

**Your answer:**

## Identify the segregation of business units across catalog as best practice

**Your answer:**
