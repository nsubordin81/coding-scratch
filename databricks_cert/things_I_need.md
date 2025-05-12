# stuff I gotta know for the databricks exam

**Section 1: Databricks Lakehouse Platform**  
Describe the relationship between the data lakehouse and the data warehouse.

--

data warehouses have limitations that the data lakehouse makes up for.
data warehouse involves dealing with data in a structured format, where there is an explicit schema. it is for setting up ETL operations where data is taken from one place, transformed and then stored elsewhere.

it seems like data lakes are taking this input data and they are somteims doing analytics on iot on the side and sometimes ML, and then they are outputting into an unstructured format.

there are things data warehhouses and the structured data afford for like better data governance. adding a metadata layer and having an interface to the data lake that involves explicit management of the data seems to be the data lakehouse compromise. data is still output unstructured, there is still flexibilty to do analytics and ML, but there is also governance and metadata management.

--

Identify the improvement in data quality in the data lakehouse over the data lake.

--

## improvement in data quality is that now instead of boing through the ETL without any explicit structure, all of the data passes through the metadata and governance layer which enforces good data quality

Compare and contrast silver and gold tables, which workloads will use a bronze table as a source, which workloads will use a gold table as a source.  
Identify elements of the Databricks Platform Architecture, such as what is located in the data plane versus the control plane and what resides in the customer’s cloud account.

--

the control plane is where you have the notebooks and other aspects of interfacing with databricks, and then there is a compute/data plane that lives in the customer's cloud account. this is the business data owned by the customer in their private cloud hosted by some cloud provider. high level to me without checking the details is that all the things you do in the presentation layer with databricks live in the control plane and are managed by databricks, and then all of the things that need to happen to interact with object storage and store the output of computations and manage resources involved in the computations lives and are manged by customers in their private cloud space.

--
Differentiate between all-purpose clusters and jobs clusters.

--

all purpose compute appears to be a dedicated cluster which is running all the time, not serverless? you have settings you figure out like the runtime environment version and the version of spark and scala that you are using. ther eis this thing called "photon acceleration" which is a way to accelerate the workload and reduce cost.

the access mode controls whether your user experiences the cluster as a single user environment with unity catalog controlling the data, as a multi-user environment with unity catalog or as an un-isolated environment with no mandatory unity catalog.

there are compute settings such as limiting what users can do with the cluster. this includes what libraries they can use, what options they can see, what settings they have,
how much cost they can incur

--
Identify how cluster software is versioned using the Databricks Runtime.

--

all that I saw here was that there are collections of standard libraries available throiugh the runtimes, you have standard for running batch jobs or etls and different language support, then you have ML runtimes which have support for pytorch and tensorflow and sklearn ans such already built in. you also have photon which is for high volume in the area of maybe pedabytes of processing to accelerate those workflows..

there seems to be more to the versioning question `shoudl look that up`

--
Identify how clusters can be filtered to view those that are accessible by the user.  
Describe how clusters are terminated and the impact of terminating a cluster.

--
you can terminate a cluster both through inactivity period setting in the cluster details page,
from the top right of the cluster details next to the start and edit buttons
from within a notebook, as a popout context from the cluster itself.

## terminating a cluster just shuts it down ans stops it running. you can also delete if you have permissions that would get rid of the cluster permanently and you would have to recreate it from scratch later

Identify a scenario in which restarting the cluster will be useful.

--
scenarios: compute cluster is overloaded or it is out of memory or it is acting in a strange way.

--
Describe how to use multiple languages within the same notebook.  
Identify how to run one notebook from within another notebook.  
Identify how notebooks can be shared with others.  
Describe how Databricks Repos enables CI/CD workflows in Databricks.  
Identify Git operations available via Databricks Repos.  
Identify limitations in Databricks Notebooks version control functionality relative to Repos.

**Section 2: ELT with Apache Spark**  
Extract data from a single file and from a directory of files.  
Identify the prefix included after the FROM keyword as the data type.  
Create a view, a temporary view, and a CTE as a reference to a file.  
Identify that tables from external sources are not Delta Lake tables.  
Create a table from a JDBC connection and from an external CSV file.  
Identify how the count if function and the count where x is null can be used.  
Identify how the count(row) skips NULL values.  
Deduplicate rows from an existing Delta Lake table.  
Create a new table from an existing table while removing duplicate rows.  
Deduplicate a row based on specific columns.  
Validate that the primary key is unique across all rows.  
Validate that a field is associated with just one unique value in another field.  
Validate that a value is not present in a specific field.  
Cast a column to a timestamp.  
Extract calendar data from a timestamp.  
Extract a specific pattern from an existing string column.  
Utilize the dot syntax to extract nested data fields.  
Identify the benefits of using array functions.  
Parse JSON strings into structs.  
Identify which result will be returned based on a join query.  
Identify a scenario to use the explode function versus the flatten function.  
Identify the PIVOT clause as a way to convert data from a long format to a wide format.  
Define a SQL UDF.  
Identify the location of a function.  
Describe the security model for sharing SQL UDFs.  
Use CASE/WHEN in SQL code.  
Leverage CASE/WHEN for custom control flow.

**Section 3: Incremental Data Processing**  
Identify where Delta Lake provides ACID transactions.  
Identify the benefits of ACID transactions.  
Identify whether a transaction is ACID-compliant.  
Compare and contrast data and metadata.  
Compare and contrast managed and external tables.  
Identify a scenario to use an external table.  
Create a managed table.  
Identify the location of a table.  
Inspect the directory structure of Delta Lake files.  
Identify who has written previous versions of a table.  
Review a history of table transactions.  
Roll back a table to a previous version.  
Identify that a table can be rolled back to a previous version.  
Query a specific version of a table.  
Identify why Zordering is beneficial to Delta Lake tables.  
Identify how vacuum commits deletes.  
Identify the kind of files Optimize compacts.  
Identify CTAS as a solution.  
Create a generated column.  
Add a table comment.  
Use CREATE OR REPLACE TABLE and INSERT OVERWRITE.  
Compare and contrast CREATE OR REPLACE TABLE and INSERT OVERWRITE.  
Identify a scenario in which MERGE should be used.  
Identify MERGE as a command to deduplicate data upon writing.  
Describe the benefits of the MERGE command.  
Identify why a COPY INTO statement is not duplicating data in the target table.  
Identify a scenario in which COPY INTO should be used.  
Use COPY INTO to insert data.  
Identify the components necessary to create a new DLT pipeline.  
Identify the purpose of the target and of the notebook libraries in creating a pipeline.  
Compare and contrast triggered and continuous pipelines in terms of cost and latency.  
Identify which source location is utilizing Auto Loader.  
Identify a scenario in which Auto Loader is beneficial.  
Identify why Auto Loader has inferred all data to be STRING from a JSON source.  
Identify the default behavior of a constraint violation.  
Identify the impact of ON VIOLATION DROP ROW and ON VIOLATION FAIL UPDATE for a constraint violation.  
Explain change data capture and the behavior of APPLY CHANGES INTO.  
Query the events log to get metrics, perform audit logging, examine lineage.  
Troubleshoot DLT syntax: Identify which notebook in a DLT pipeline produced an error, identify the need for LIVE in create statement, identify the need for STREAM in from clause.

**Section 4: Production Pipelines**  
Identify the benefits of using multiple tasks in Jobs.  
Set up a predecessor task in Jobs.  
Identify a scenario in which a predecessor task should be set up.  
Review a task's execution history.  
Identify CRON as a scheduling opportunity.  
Debug a failed task.  
Set up a retry policy in case of failure.  
Create an alert in the case of a failed task.  
Identify that an alert can be sent via email.

**Section 5: Data Governance**  
Identify one of the four areas of data governance.  
Compare and contrast metastores and catalogs.  
Identify Unity Catalog securables.  
Define a service principal.  
Identify the cluster security modes compatible with Unity Catalog.  
Create a UC-enabled all-purpose cluster.  
Create a DBSQL warehouse.  
Identify how to query a three-layer namespace.  
Implement data object access control.  
Identify colocating metastores with a workspace as best practice.  
Identify using service principals for connections as best practice.  
Identify the segregation of business units across catalog as best practice.
