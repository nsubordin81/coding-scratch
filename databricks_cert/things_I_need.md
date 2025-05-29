# Section 1: Databricks Lakehouse Platform

## Describe the relationship between the data lakehouse and the data warehouse

**Your answer:**

data warehouse was a traditional way of running thigns in the past, it is useful especially for running large ETL jobs that output structured data. it is not as flexible for things like general purpose analytics with unstructured data, data exploration at scale that kind of thing. the data lake kind of has become a different architecture that allows data to be completely unstructured and is more flexible for doing work with data that doesn't require a structured output, but it lacks the governance and structure and controls and explicit schema of a data warehose. the data lakehose marries these two concepts with a metadata and governance layer that abstracts between all of the compute and the interactions so ML and analysis work from a customer lives alongside etl jobs and batch processign work and they both go through the same data quality checks but they can be flexible to support less structure in the data during and after processing.

data lakehouse combines the good governance and performance of a data warehouse with the openness, flexibility and machine learning support of a data lake.

## Identify the improvement in data quality in the data lakehouse over the data lake

**Your answer:**
the improvement would be the metadata and access layer. `note to self look this up and be able to articulate it better, you still haven't grokked it`
but maybe this is enough, data governance.

## Compare and contrast silver and gold tables, which workloads will use a bronze table as a source, which workloads will use a gold table as a source

**Your answer:**

## Identify elements of the Databricks Platform Architecture, such as what is located in the data plane versus the control plane and what resides in the customer’s cloud account

**Your answer:**
the 'data plane' is also I thinkt he compute plane which is what the customer's cloud account holds. it is actually the cloud resources that are providing the storage and the compute, they are managed and owned by the customer. this means that the vendor, databricks and amazon or azure or whoever, is already guaranteeing that the business sensitive data resides in an area totally managed byt he customer, and they have control and ownership for what they are working with. the control plan is where the batch and etl jobs, the cluster management, the notebooks, all of the things that I guess you would consider presentation are living. databricks manages that part, which is quite a bit to abstract away from the ucustomer, how spark and databricks interfaces interact with the cloud computer resources. the outputs are also on the compute plane so data only lives in the control plane as long as it needs to be stored in memory. `note you don't know exactly where the boundary is here`

so the architecture consists of the cloud infrastructure which could be any of the 3 major providers, aws, google or azure. that is where databricks provisions the nodes, this is part of the data plane, the nodes in the cluster are all built with the components of the databricks runtime which includes thingns like spark and delta lake. that is bundled into the node as software. this is still the data plane. the control plane lives on top of that and is where you interact with databricks. it has notebooks, workspaces, jobs, batch and etl, and dashboards and the like. this is also where you ahve cluster manager, workflow management interfaces.

the data plane is storage (databricks file system) and computer (virtual machines and clusters) it will use the subscriber's cloud account to provision.

## Differentiate between all-purpose clusters and jobs clusters

**Your answer:**
all purpose clusters are long running, they are meant to be for things like notebooks that live a while with the data, jobs that are shared by many users. they will have maybe less memory and compute power because they will be running and incurring cost longer, they are for data exploration and availability. job clusters are for things like bartch jobs and etls that run and then automatically stop and clean themselves up, they are configured for one, narrow job.

## Identify how cluster software is versioned using the Databricks Runtime

**Your answer:**
`not sure if I really have the answer to this one yet` what I do know is taht there are different types of runtimes that support different purposes for clusters. one ist he standard which is for most purposes. it contains prebuilt libraries for working with data in whatever of the supported langauges you want to work in. there is a scala version a spark version and an overall databricks version with each runtime. in addition to the standard flavor, there is the flavor for doing faster jobs, to accelerate the processing, this is called the photon processor. the next flavor after this is the ML flavor, and it supports machine learning with libraries pre installed like pytorch, tensorflow, and others like sklearn and scipy numpy and pandas. the runtimes make it so that you don't have to install a lot of packages when you work with a cluster, they are already there.

## Identify how clusters can be filtered to view those that are accessible by the user

**Your answer:**
there are a few ways. there is a search bar in the databricks UI that allows you to filter clusters by owner column. you can also use the databricks CLI in your shell to filter the json that comes from the databricks clusters get <id> command.

## Describe how clusters are terminated and the impact of terminating a cluster

**Your answer:**
termination of a cluster if you have the rights to do so can be done oa few differnet ways. first, you can terminate it with a button in the upper right of the scren when you are looking at the compute, then you can also terminate it by going into the cluster and then there is a context menu where you can see the different options available to you one of them is to terminate. I bet you could also do it through the CLI. termination is not the same as deletion. termination just shuts down the cluster so it isn't consuming resources, it can be started up again later. deletion actually wipes the cluster and its configuration gets removed.

## Identify a scenario in which restarting the cluster will be useful

**Your answer:**
you can restart a cluster when it runs out of memory or if it becomes corrupted in some way and is providing output that is not aligned to what you expect, maybe there is some residual data interfering with its function that is in memory or somewhere that is affecting the job output. you can restart from many of the same menus that you can terminate from.

## Describe how to use multiple languages within the same notebook

**Your answer:**

This whole thing I describe below are known as 'magic commands' they let you express yourself in a different language than the default one of the notebook. they are like escape sequences to tell whatever is interpreting your code you want to do something different.

you can use python scala, R, sql and even bash. you can also use the magic % sign with the name of the language you want to use e.g. the bash or shell is hidden within the python one with !ls
the other notebook magic are %r, %scala %python %sql %md

Not related to this answer but I needed a bplace to put it, command or ctrl + option or alt + space will give you suggestions for how to finish sql queries or python code.

the default language of the notebook is set at the top of the notebook, all new code cells will use that language first and then you would switch it.

## Identify how to run one notebook from within another notebook

**Your answer:**
first of all, it is beneficial to organize your notebooks in your workspace under different directories. when you do this you can reference them by location relative to other notebooks in the workspace.

but that isn't the answer. to run notebooks from other notebooks there is a special magic command called `%run`. you can use this to import another notebook by absolute or relative path into your current notebook. any functions or variables or classes you declare in that notebook becomes available in the notebook that imports it.

another magicd command not gone over in the test criteria but is good to know about is %fs. you can list the contents of diretories with it %fs ls <directory as string>

you can also use dbutils for this. but dbutils can do a ton more. it can do

- credentials management
- filesystem stuff
- dataset understanding (I guess descriptive stats and stuff)
- managing jobs
- managing sesison isolated libraries, not quite sure what those are
- something about input widgets
- a bunch of experimental stuff that they want to support like interacting with a host computer and impact notebook control flow and preview stuff.

if I had to sum it up I would say that filesystem utilities and secrets management utilities are the most important and official capabilities of these utilities
and they are bgetter than the magic commands because they can interact with python you can send their output as input to python functions directly.

## Identify how notebooks can be shared with others

**Your answer:**
there is a share button in the intervface. there are differennt levels of access you can choose, like view which is read only, run which allows to run the notebook but not edit it, edit, or manage which allows people to change which cluster it runs with and delete it etc. you can choose individuals or roles in the system that are allowed to do the things, roles would be like admin.

## Describe how Databricks Repos enables CI/CD workflows in Databricks

**Your answer:**

## Identify Git operations available via Databricks Repos

**Your answer:**
guessing add, commit, push, not sure which wouldn't be to be honest, would it be all standard git terminal commands? are there any missing `look this up`

actual answer form the course seems to be you can create new branches, you can pull from github origin, you can commit changes to a branch. merging appears to only be done via the remote git repository.

## Identify limitations in Databricks Notebooks version control functionality relative to Repos

**Your answer:**
a databricks notebook is more like autosave I imagine, where a state of your notebook is automatically saved at some point while you work on it and you can only recover from those snapshots. it is also harder to share older versions of a notebook with someone potentially because you can only save that notebook in its version without saving the entire contents of the directory the notebook is in. if you want to version an entire directory and all objects contained within it the way you would with git, that is only avaiable through version control. you wouldn't synchronize the version history of one notebook with another and have one commit to represent the state of all objects at that point in time.

so after going nover this in the course I'm taking now, can confirm I was more or less right. there is an autosave and version history feature ffor notebooks built into databricks, which allows someone to delete history files from anywhere int he history and doesn't support branching or merging, it just creates a fresh copy of the file periodically during changes which is not explicitly managed. you can go to history but you don't have the amount of control you get with git's distrubuted version control, nor do you have the safety that the files are actually backed up.

# Section 2: ELT with Apache Spark

## Extract data from a single file and from a directory of files

**Your answer:**
one thing you can do is open the terminal and use linux commands to navigate the databricks file system /dbfs/

this feels like you can do it with a sql query against it, but haven't tried yet not as sure of the anatomy. keep having to start a data warehouse to figure it out. a bit worried about a slap on the wrist for that.

## Identify the prefix included after the FROM keyword as the data type

**Your answer:**
is that the schema? I'm not sure what this is asking it seems like this is the table name, after from it woudl typically be 'schema.tablename' but maybe spark sql is different.

## Create a view, a temporary view, and a CTE as a reference to a file

**Your answer:**

## Identify that tables from external sources are not Delta Lake tables

**Your answer:**
the 'type' field in the details will be 'Managed' for a delta lake table, it will be 'EXTERNAL' for an external table not managed by delta lake. also you can't OPTMIZE command an external table that isn't delta lake. if you want to, you can do a create table command using delta from some existing table.

## Create a table from a JDBC connection and from an external CSV file

**Your answer:**
I think based on my training that you can do this with the sql editor and the catalog explorer. find reference to the table in the external filesystem by path and then use a create table command in the sql editor targeting this path and with 'using csv' with {} around the path. e..g.

```
create table my_aweseome_table
using csv
options { path ""
header "true"
}
```

by default it will put it in the default schema

even easier potentially is to use the catalog explorer to add an external file which can be3 a file from your filesystem and when you do that you whill have an option to automatically create a table from that file which will be dropped into the catalog explorer.

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
first of all, delta lake is a new automated etl pipelining tool that is declarative and automates portions fo data pipelining, helping to address some of the issues that existed with the prior data warehousing etl challenges, including messy and specific and brittle pipelines that were more imperative and manual and contained a lot of custom manual coding to patch them togetehr, were not flexible to doing stream and batch processing as alternatives.

ok, here is the real answer I believe. the ACID transactions happen in the delta lake's writer process, which writes the table contents to parquet files and then writes the transaction information like predicates and `other information` to the transaction log as a json file.

## Identify the benefits of ACID transactions

**Your answer:**
first the features. ACID is
Atomicity - all operations within a transaction happen or don't as a unit
Consistency - you are transforming the data from one valid state to another, not leaving things in an invalid state for a time
Isolation - your transactions happening concurrently with other transactions aren't impacted by the state changes they are making wrt one another
Durability - once data has been committed, it doesnt' change or disappear, it is there for the long haul

these standards lead to the highest reliability you can have. you are fault tolerant because you have durable logs, you can guarantee that if a transaction succeeded the data is there

## Identify whether a transaction is ACID-compliant

**Your answer:**
well I assume I'd use the above criteria to see if the transaction was able to meet it.

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
if you ahve a high cardinality to your data, similar data will be stored nearby other similar data, ther eis less overall data to traverse for the delta lake in order to retrieve it, your queries will be faster, and it is an incremental process so you can rerun it after data is added and it will only impact the new records and associations back to historical data.

I don't know where this fits in so I will just write it here. htere are delta live tables or maybe just pipielins now which are ways to set up workflows using the delta lake. you can set up the type of job, whether it is development or production, what cluster it will use, whether it will be continuous or triggered by some event, and what table the ingest will go to. you then have a way to look at your pipelines and see what type of job it is that is feeding your tables, and inspect the portions of the ETL that you are doing and what the outputs are and where they go to.

similarly with delta live tables, you have different components, like bronze, silver and gold.

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
you can change the type of cluster runtime, library dependencies for a task at the task level. you can get more granular feedback for where in a job a failure occurs because there are dependencies based on tasks, you can isolate the workload being taken on and potentially resume jobs from tasks that haven't completed, you can potentially have tasks take place concurrently within a workflow.

## Set up a predecessor task in Jobs

**Your answer:**

## Identify a scenario in which a predecessor task should be set up

**Your answer:**

## Review a task's execution history

**Your answer:**
` I feel like I learned this from the jobs overview but I don't remember what it is`

## Identify CRON as a scheduling opportunity

**Your answer:**
you can use CRON syntax for scheduling dashboards or jobs. I'm not sure what this is revereing to other than using CRON language to schedule jobs for recurrent tasks.

## Debug a failed task

**Your answer:**
debugging failed tasks would happen in the more detailed job runs screen where you can view the error log output for the task and troubleshoot from there.

you can navigate to teh task level from a job that failed and you can even set up an if/else follow on condition that has different branches for handling success or failure after a task has
failed based on that type of failure if you ahve a proogrammatic way of proceeding.

## Set up a retry policy in case of failure

**Your answer:**
seems pretty easy. go into the job, go into the tasks flow, find a task that you want to create a retry policy for, there is a retries button there is a configuraiton dialog wyou can set up the number of times and the backoff in a gui, you can have unlimited, you can also check a box for retry on time-out.

## Create an alert in the case of a failed task

**Your answer:**
there is a notifications optiojn above the retries option where you can set the notification channels destinations configured by your workspace administrator, you can set up whether the notification is for failure, for something happening for a duration, for startingt or successful completion or failure, or ran too long or streaming backlog though I don't know that that means. if you skip a run or cancel it it you can notify or opt to not notify, and you can wait to notify until the last task retry. bytes of unconsumed data across all streams, so that is a big backlogt of streams, or files or records. so kind of like if kafka was not getting things across fast enough.

## Identify that an alert can be sent via email

**Your answer:**
yep, I see it there in the list of potential destinations

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

```

```

# Extra STuff to know

- databricks is based on Spark, made by the same folks
- databricks is a distributed data processing platform which is what spark is too
- it is also an in-memory processing platform, spark is that, databricks is still that. so it is more performant than, say, mapreduce
- databricks file system is an abstraction for persistent storage. dbfs let's you deal with files in teh cluster in a distributed and shared manner among nodes, however, even though the representation of these files in dbfs makes it look like theya re stored in the cluster, they are actually stored in persistent cloude storage in your cloud provider's object storage solution.

## cluster config

you can do a multi node or single node cluster

- for multi-node you can choose to let other acces but you are restricted to python and spark sql languages
- dedicated is using it by yourself
- you can pick a node type which determines how much compute you get
- you pay in DBUs which are right now priced at $0.40 / hr .
- if you do multi node you can configure compute to be the same or different form the driver node in terms of VM power, and you can set up max and min scale for how many nodes to autoscale with
- community edition doesn't let you configure all these things it just lets you pick the runtime and defaults your computer to a standard value

## what and why delta lake?

delta lake is a storage frameowrk for databricks that helps with some data lake problems.

what problems?
data lakes can have inconsistency (makes sense they are typically BASE not ACID transactions)
data lakes can have performance problems

while delta lake is not a format but a framework, delta table is a format and it is the default schema used for spark sql in databricks.

when you execute an insert statement, you are (language is important here for correctness) "adding a new parquet file to the delta table directory for your table."

## more stuff about delta lake.

parquet file are immutable and the engine just appends them and then uses the transaction log to derive the current state. it is very event sourcing remeniscient.
you will have appends. it will only make one parquet for a single insert query with several records, but for update queries you will have one parquet file appended per updated record.
older file updates will become obselete and the engine will know which ones to review in order to build current state based on if the transactions in those files are still relevant.
I think for the example he showed it was supposed to show that there were 4 files before and after the update because we added two for the update but then we didn't need the other 2 insertion ones anymore since those records had since changed. so it is keeping track of the deltas.

in my case there was file compation so I couldn't properly deduce from numbe rof transactions.
the history command as it turns out for a delta table

let's just enumerage important commands I learned:

describe detail <table>
describe history <table> - see how the json log evolved over time indicating how the parquet files were restructured for versions

%fs ls "databricks filesystem location" - look at the files

there are advanced features of delta lake involving time machine, in other words being able to query the version history or the timestamp of earlier states of teh delta table
the syntax for that is

timestamp as of
version as of <number>

you can also use restore to get things back from an earlier version:

restore table <tablename> to @v
restore table <tablename> to version as of
restore table <tablename> to timestamp as of

you can also optimize the parquet files. it is generally bad for performance to have several small parquets with individual operations/transactions represented in each. optimize will consolidate them into a single parquet.

when you use zorder by <column name> , you can bucket the resulting parquets such that records with similar data for that column are closer together, which will optimize read performance by a whole lot.

and when you konw things are out of date, you can vacuum to garbage collect old parquets you don' tneed anymore

vacuum <tablename> <retention period>

default retention policy is 7 days so if you don't specify one it tries that one and it can't be younger change than that or it won't do anything

to go lower than that you need to do an alter table on your table and use a spark configuration param to set the retention duration to a lower amount. this should really never be done execpt in very special circumstances or with test data you aren't worried about losing.

we are talking about hard deleting data from a system that is pretty much event sourced, which is a dangerous operation.

once you garbage collect, you can't restore any more.

### relational storage active recall

relational storage in databricks is done with metadata in the hive metastore

instead of being stored as tables, the data is stored as metadata in this metastore and then you get data that corresponds to it living in the databricks file system. the dbfs woudl be overlaid on whatever cloud provider object storage solution you have.

When you create a table with a typical `CREATE TABLE` statement, it is stored in the central Hive metastore. By default, the table's metadata is placed in the `default` database (which is also a schema), and the corresponding data is stored in the `/user/hive/warehouse` directory on the Databricks File System (DBFS).

If you create a table within a specified schema, the Hive metastore will create a subdirectory for that schema in the warehouse directory, with the schema name suffixed by `.db`. For example, creating a schema named `sales` will result in a directory `/user/hive/warehouse/sales.db`, and all tables within that schema will be nested inside this directory.

Additionally, you can specify a custom path in DBFS as part of your `CREATE TABLE` statement. In this case, the table's metadata will still reside in the Hive metastore, but the table's data will be stored in the specified location, outside the default `/user/hive/warehouse` path. you do this with the `location` keyword in the create schema statement, specifying the path you can to create in dbfs

### external tables and managed tables:

conceptual difference, managed tables are cases where the underlying table data is stored in dbfs through a create table statement that didn't specify an alternative location, so the location is synced between the table metadata in the hive metastore and the underlying dbfs. if you drop a managed table, the undlerlying data will be dropped too by databricks. external tables have underlying data that doesn't live in the schema directory on dbfs that corresponds to the metastore's schema. if you drop an external table, the hive metastore data gets dropped, but the underlying data in dbfs is retained.

useful, `describe extended <tablename> ` gives you more table information

'MANAGED' and 'EXTERNAL'

CREATE SCHEMA and CREATE DATABASE are the same in databricks, do the same thing, both are creating directories in the hive metastore and hive warehouse

describe extended defaults ot describing tables, you can also do `describe database extended` to describe a schema/database in hive
remember that foldersin dbfs that are schemas get a .db at the end by convention in databricks, databricks does this foer you

ok, so just did a bunch of drills on this and feelaing pretty comfortable with it now

one key thing I learned is that the managed tables vs. external tables thing transcends location in dbfs, but not usage of the `location` keyword. accidental experiment confirmed you can use the location keyword and specify the exact same location on dbfs that the managed woudl automatically save to, but it is still flagged as an external table and that still leads to it retaining the data when you drop the table and only dropping the metadata.

### ctas statements

this is createing a table by getting query results form another table.
you can't specify schema info, that is, you can't assign datatypes to the columns in the query, it has to be inferred
you can add things like `comments` `partitioned by` and `location` to specify information about how the underlying data fo the newly created table should be stored and described
these are created with the data, not insert statements, you ren't just createing the ttable schema you care3 createing the data from the other table pulled in also

### constraints

you can add constratints to existing delta tables

you can only add `not null` and `check` constraints. `check` uses condotionals that are like where clauses

constraints must already be met by all existing data in the table if not empty

new data that fails constrints will result in write failure

syntax is `alter table` table ` add constraint` constraint name ` check` condition

### deep and shallow cloning of delta tables

syntax is super easy
`create table` clone table name
`deep copy` source table name

or
`shallow copy` source table name

the difference between them: deep copy creates a copy of all underlying data
shallow copy only creates copy of the delta transaction logs for the table, no data is being copied, much faster

deep copi es for large tables can take a really long time, but htey can be done incrementally and pick up changes as they are being made in flight

important point, you never risk data in the source tables getting corrupted or overwritten while doing these, because in both cases they clone in a different location than the source tables.

### views

these are really just stored sql queries of other tables, but you can query them like tables. they have no actual data in them stored, they are queries that are run every time you query against them

three kinds are stored, temporary and global. what do you think those are? stored would probably be queries taht are saved somewehre in the schema where you can actually see them represented, temporary are maybe ones that you do inline in another query, and global would be I suppose ones that are avaiablel from anywhere, any database or location in the hive metastore???

let's see what the answer really was:
ok, so the real answer is that the stored views are persistently stored in the underlying filesystem, and the temp views are ones that are only around for that spark session

four places where you can see new spark sessions created:

- open a notebook
- detach and reattach to a cluster
- installing a new python package (interesting). this is because the python interpreter is restarted
- restarting a spark cluster

I guess my question is why do these kickoff new spark sessions, but I can hold it. ok actually I think I can answer it because all 4 involve having a new python interpreter kernel start, so less to do with the cluster status and more to do with the runtime environment changes caused by that compute becming available and unavailable.

ok, another thing, it is not 'global view' it is 'global_temp' or global temporary view. these are available to any notebook running on the currently active databricks cluster. it is good to know that these are only available for the lifetime of the cluster and they have to be qualified when you use them with the global_temp keyword, much as you would qualify a schema in the sql statements.

the scope is probalby the best way to remember
stored view - database scope, must be manuyally dropped with ta 'drop view' command
temp view - session scope for spark, dropped automatically when spark session terminates
global temp view - cluster scope, dropped when the cluster is terminated or restarted. also these can be accessed for multiple spark sessions as long as the cluster is still running

### extract data from files with spark sql

select \* from file_format.`path_to_file`

backticks are important

can do something like
select _ from json.`path_to_file`
seelct _ from parquet.`path_to_file`

file formats supported and good for raw text extraction are (JSON, CSV, TSV, TXT)
select \* from text.`path_to_file`
self-describing formats like json work better than something like CSV

can do bytes for unstructured data or things already stored in binary
select \* from binaryFile.`path_to_file`

getting them into the data lakehouse

from files into delta_tables we can use
create table my_awesome table
as select \* from json.`path_to_file`

so just like creating delta tables from other delta tables, you can't explicilty state teh schema in your query
you have to let the ctas statement infer it. this means that if there isn't good inherent schema or self-description in the
file format itself, then you will be hard pressed to load it into a table with the correct datatypes.

csv and tsv not great candidates for that then.

you also can't specify file options that yo migh twant to with something like a csv file.
what you can do instead is have a create table statement with the using keyword to get back the missing file options

important stuff, when you go this route, you have to use a location keyword, meaning that you aren't going to be storing this table in the delta lake, the hive metastore, what have you

also, the table is not converted to a delta table, there is no data movement, you aren't creating a transaction log, this is just a reference to an external csv in another location

create table external
(id int, name string)
using data_source
options (header="true",
delimiter=";")
location=path

ok, so this makes it seem like there is an inherent weakness with using delta tables in databricks when you have external formats without good schema definitionss.

but it turns out that once you have created this external table with a defined schema, you can then create a temp view off of that schema and then use a ctas off of that temp view to read the table in as a delta lake table. seems like a lot of hops with known steps, I wonder why nobody has automated this yet.

### notes from hands on practice with these:

csv version of extracting the data didn't work because the delimiter was a semicolon
note that for csv as datasource column order and datatypes of columns should not get shuyffled in the csv as you update it.

demonstration though when we used the option of ctas with using csv command that we created an external table that was not a delta table.
the way to prove that this had happened and we didn't get the benefits. that it happened: describe extended books shows that it is in the external location
we didn't get the benefits: we copied the rows back into a csv that was twice as long saving them into the table using a spark api, and this should have doubled the tablesize but
instead spark still read from the cache, because there were no delta tables configuration to tell it to update. refresh table command invalidates teh cache and rescans the dataset and bring everything back into memory which can take a really long time. that is th elocal storage cache

### updating and overriding files

with delta tables it is often better to overwrite, because

1. you retain the older data and cdan get it back with time travel
2. it is faster because a delete and recreate would invovle recursive directory listing and other operations that you don't need if you don't delete the full table
3. it is an atomic operation, so you can concurrently read from or write to a table's existing contents even while it is being replaced
4. since this is ACID, the whole operation will revert if failed

the way to take advantage of this for updates is to use a CRAS statement `create or replace table as`

`insert overwrite` is another operation which has the same net effect as CRAS

differences:
shows up as a write with mode overwrite
can't create a new table only overwrite an existing one
is safer because it will only add new records that match the schema of the existing table wheras CRAS might accidentally add or remove columns when it creates teh new table or replaces it

for adding new records, that is `insert into` , but there is one problem with that, it will keep inserting into the table and not worry about duplicates.

### advanced transformations

spark sql has ways to directly work with json data stored as a string in a column. you can use the ':' colon delimiter to drill down into json properties of string json objects, even nested ones

e.g. `profile:address:country` will get you the country field of the address nested object in the profile json string

you can also use a spark sql datatype called a profile_struct, which will transform the text json into a type that is aware of the structure of, in this example, the json text. it will allow you to browse the data like it was a parsed json in the query outputs, and also you can query it with dot syntax instead of colon syntax.

it is harder to get to though, you use a ctas or cras to get to it, but you have to provide a schema. in many cases you don't have one, but one row of data from that column in your original text table shoudl provide spark what it needs, you use the `schema_of_json` to capture this in the query. remember yoiu also use the `from_json` in there to get the json parsed in the first place.

the parsed_struct also has a .\* feature which can flatten all of the fields in the top layer of the struct also useful.

explode() spark sql function will explode an array column and make a row for each entry of the array, duplicating the other columns of the table

collect_set() spark function will collect elements of the array and only have it keep one copy of each element, remove duplicates. this consolidates an array into a set.
if the array is nested, like 2d, then we ahve to think a bit more about it. the solution there is to use `flatten` and then wrap that in `array_distinct` to keep only the distinct values

so what is the difference between collect_set and array_distinct? well collect_set() as an aggregate fuunction works on more than just arrays and additionally it can recognize duplicate collections like arrays where the values and order are the same and only keep one of those. array_distinct is just to remove duplicate values from a 1d array of values.

#### joins supported by spark

inner, outer, left, right, anti, cross, semi

#### set operations supported by spark

union, intersect and minus (difference)

union puts all rows whether they are in one or the other
intersect only records that are in both
minus only records that are in a but not b

pivot clause changes data perspective. so I'm not as familiar but it seems like you take some column and do an aggregate function on the data so that the data result gets flattened out for the targt column across some valeus for that column. in the example it was to take the orders_enriched table and then pivot it out to show the sum of the quantity of books ordered for each customer for 12 of the books in the book column. just selecting from orders would not do this, becasue it has an array in the books column.

### Higher order function and UDFs user defined functions

why do you need higher order functiosn?
to work with complex datatypes in columns, like and array of structtypes, i.e. hierarchial data

after the filter you might want to run a subquery (wrapper) to use a where clause on the result

udf allows you to make a custom combination of sql queries avaialble as a function in the database making them reasonable in sql queries
they maintain the benefits of spark

what you need for UDF

`create or replace function` then name of function, parameters with types
type for the data to be returned

function body

UDFs are permanent functions taht are persisted to the database and so you can use them across different spark sessions and notebooks

you can drop a udf with `drop function`

## spark data streaming

data stream is any source that grows over time

- files in cloud storage
- database updates in a change data capture feed (CDC)
- events in a pub/sub message feed

two approaches essentailly with some intermeidate variants

- process every record every time you need to, so like a batch
- process only what is added as it comes in

you can use structured streaming in spark for handling the data as it comes in
abstractly, spark structured streaming is able to handle an infinite incoming data stream.
it treats the stream incremental elements like they are rows in an unbounded table.

you can write these outputs of transformations on this table to a delta table or many other types of storage.

for delta tables, you can use spark readStream to set up the delta table source as an outgoing stream, and you get a streamDF dataframe to operate on
it will handle the data that is coming in as well as hwat is already there.

you use writeStream function off of the spark streamDF to poll incrementally for added records and process them, and then to append to the table, and the whole thing is enabled by checkpoints that are set up to monitor the changes to the tables.

options for processingTime,

- with no .trigger, default will be processed every 500 milliseconds
- with .trigger you can put a processingTime to a set interval time
- with .trigger once=True, you can batch process all records currently in table
- with .trigger availableNow=True, you can microbatch several batches for immediate processing

outputMode has two options, "append" and "complete" . these have to do with what happens to the result table. in the first case, the result table is appended to, in the second case, the result table is overwritten each time.

checkpoints track stream progress, they should not be shared between streams, they are particular to the progress of one stream.
there are also write ahead logs. this creates fault tolerance. the write ahead is done as offsets of records to process vs already processed per time interval. this is like kafka's producers

stream transformations are designed for exactly once delivery, they infrasttructure and the operatios are idempotent so even if you process somethign more than once it will only have the impact as if you processed it once.

you need a repeatable source storage to make this all work though, so in other words s3 or kafka or something like that, where you could go and get the records and play them back all over again.

j8ust as an fyi, you can't sort or deduplicate with streaming data. this is apparently really hard. there are advanced methods like windowing and watermarking

### form the hands on exercise

- you create a streaming view using the spark.readStream method you can use a delta table as a stream source and then create a temporary view off of it
- in the exercise we then select from this view but in practice you wouldn't becuase it leads to an active polling in the display. you might for dashboards, but for static demos you probably don't want to.

you can't do order by becausae that is sorting and not supported for streams.

something to understand about how spark manages streaming. you need to support incremental logic form the beginning with the read stream in order for spark to know taht it shoudl be using a streaming dataframe for the writing process toi write into the correct kind of dataframe.

streaming queries are always on queries that can have interactive dashboards associated with them. the streaming queries are queries against a streaming data source, like a temp view that is streaming or a streaming table or dataframe. once something is written to durable storage it is no longer a streaming query to query it it will return an absolute snapshot value of the table at that point in time.

careful to always terminate your streaming queries because if they stay on the clusters can't autoterminate

important takeaway for me, you have the writestream queries on, and they need to stay on to pick up changes that occur. but you shouldn't leave them on when testing. you can also do the batch mode with the trigger once=True or availableNow=True, and it will do all available and then terminate itself.

## incremental data ingestion from files in databricks

files that have been encountered since the last ingestion. this is to me like microbatching and things like that. it just means what we were trying to do on the FINCH project where we only processed new records and not reprocessed all the old records.

spark has two ways to efficiently procewss and store things as they come in

- copy into spark sql command
- autoloader

copy into

- idempotent
- incremental

syntax

`copy into` <table>
`from` <file path>
`format` e.g. csv
`format_options` things like delimiter=":"
`copy_option` things like mergeSchema=True

autoloader

this option is for processing files as they arrive into a storage location efficiently.
can work at the scale of billions
near realtime performance in the millions of files processed per hour
uses checkpointing the same way kafka uses offsets and such, it can ensure exactly once delivery and can resume from where it left off

syntax of autoloader

`spark.readStream
        .format("cloudFiles")
        .option("cloudFiles.format", <source format>)
        .load(<path-to-files>)
      .writeStream
        .option("checkpoint_location", <checkpoint_directory>)
        .table(<table_name>)
`

one other thing you an specify during read to avoid the inference cost for when autoloader auto-detects the schema of the incoming files
is to provide a cloudFiles.schemaLocation option. this will make it so that the schema is known and doesn't need to be inferred every time a new file is read in.
you can put this in the same place as your checkpoint to store the metadata needed for incremental processing.

overall the difference between these two approaches boils down to convenience vs. scalability. autoloader can process in batches so can work at scale, and copy into is probably easier to set up because you can do it as a simple query and I guess don't necessarily need to set up a dedicated location in cloud storage to ingest from, but rather specify a file location to ingest from.

the readStream and writeStream calls are part of the structured streaming api

## Multi Hop Architecture

Medallion architecture is another name for it
this is a design pattern to logically organizing data in a multi layered approach

the idea is for incremental improvement of the structure and quality of the data as it flows from layer to layer of the architecture

bronze is the raw data coming in
json files, operational databases (transactional oltp), or kafka streams

silver layer of the architecture involves filtering cleaning, augmenting of data
can be joined fields

gold layer has aggregated data used for reporting, dashboarding and machine learning

benefits

- simple
- can recreate tables from raw data at any time, so repeatable I guess
- supports batch and streaming and hybrid appraoches.

somethign I didn't grasp before, the schemaLocation doesn't preexist, it is where the first inferred schema will be cached, that is why you can put it with the checkpoint location

int he medallion example, first thing he does is set up a temp view based on a cloudFile stream with autoloader off of the source file location. he then wraps the raw stream view with another one he creates in order to add some metadata such as the current timestamp for when it arrived adn the source file name using a function I guess from spark sql called input_file_name()

## delta live tables

framework, reliable ETL data pipelines. good for quality of data
loking at it visually they are simple to read. pipieline nodes are tables bronze, silver and gold layers read left to right

multi-hop architecture is the medallion thing, just another word

delta live tables are always preceded by 'live' keyword

for streaming delta live tables you need to use the stream method in spark and the stream keyword when defining them with spark sql

you need to use the live prefix for any dlts in your queries, such as when setting up a silver layer

there are constraints you can add to your query in DLT, adn three different handlers. for all three, you start with `on violation`, then `drop row` will remove rows that violate the constraint, `fail update` will make the whole pipeline faile for a violation, and if you omit the on violatiohn clause then the behavior will be to will keep the records processed in there but log the violation

config is straightforward,
triggered or continuous
it makes a new cluster
you set up where the data files come from

cluster mode fixed size single node

when you create the pipeline with the declarative notebook and launch it, you can choose development mode or production mode. in production mode, the cluster will be regenerated for every change, while development mode allows for in place updates. somethign also about retries, either they are disabled or enabled in development mode, I think disabled, so that errors can be quickkly triaged without haveing to worry about the system trying to self-heal

you run pipieline the first time and it taks a bit to spin up the cluster, but then you see the green flowing through the nodes in the scene graph type doohickey and you know you are aoff to the races.
pipeline events, info, warn, error are all in a log at the bottome of the screen adn then on the right you have informationa bout the pipeline and then scroll down for information about the cluster compute resources. Scene graph doohickey is a DAG

clickjing a node in the pipeline shows data about it like run status, schema, comments. in silver it has a data quality readout with a visualiztion. this is because of the constraints we added

if you forget to add the live namespace, it won't fail int he declarative part in the notebook, but when you run the pipeline it will fail because it won't be able to find the table

during configuration you specify a location in dbfs that will hold all of the events that dlt logs when the pipeline runs. you can explore that directory space and find out what is happenidn in dlt when the pipeline runs.

using the dbutils or fs magic string you can look at the directory and see
autoloader/
system/
checkpoints/
tables/

system/ has all the events and if you query it you will notice that the events are stored in a delta table by DLT
tables/ has the delta live tables files storage

if you want to interact with the database that fronts those tables, you can get it

from the piptline view, wehn you click a table node in the opiopeline it will give you the query against the table's hive metastore information and you can run that.

you can stop all the streaming jobs by terminating the pipeline cluster from the job pipelines tab

## change data capture

what is it? identifying changes to a data source and delivering them to a target

structure and syntax

`apply changes into` live.target_table
from stream (live.source_table_cdc_feed)
keys (key_fields)
apply as delete when operation_field="delete"
sequence_by sequence field
columns \*

sequencing key provided by user, cdc able to make sure deleted rows don't show up downstream and updates are made in the rightr order

if you don't specify anything, it assumes upsert functionality is desired and both inserts and updates will be flowing in

the apply as delete when field is optional
you can use `except` to filter columns you don' twant to be put in the target table

you can choose with apply changes into to have one of two slowly changing dimension or SCD type tables. the default is SCD type 1 which holds two constraints:

- the table will only ever have one record per unique key
- updates to records will overwrite original information.

there is one big disadvantage of using apply changes into for a change data capture with delta live tables: the rule for delta tables that they have to be append only is broken because of the overwriting in place, and that means you can't stream from these tables as a source in the next layer of your multi hop architecture. you can still load there data into a table, but it has to be as a one time operation, like with a ctas statement

you can create live views in delta live tables. their data isn't stored to the hive metastore, but you can report on it and treat it as you would any other table for querying purposes.

the 'live' namespace in delta live tables allows you to reference tables or views created in one notebook from another notebook because they are both in the live. namespace, which is at the delta live level fo abstraction or scoping rather than the individual notebook.

to add a notebook, from your DLT pipoeline's page, you go to settings, and then press 'add notebook library' and then browse to and pick your other notebook. that is how you can end up with several referenced notebooks in the pipeline.

if you run into problems getting a DLT pipeline to run after making significant changes, you can instead of pressing start, choose the option for a 'full pipoeline refresh' which will clear all data and attempt to load it all again from streaming sources.

## pipeline jobs

building dag pipeline jobs is very gui ijntensive but it is not dinfferent in principle from what you did with prefect. you go through the process of crea ting a new job, you point the job to a notebook, you specify the location of it (like workspace or github) and then the path to the notebook you want to run, you pick a cluster, using a job cluster is better for optimizing cost.

you can have a job carry out a task within ght scope of the notebook, you can have it depend on other tasks as well so they flow sequentially. you can pass it a different value than notebook if instead of running notebook commands you want to do something like run an entire ETL pipeline, a delta live tables pipeline, etc.

the jobs details on the

for these jobs now, you can set a schedule for when they will happen. you can use a nice interface that is closer toi like a calendar appointment tool, or you can use a CRON syntax to do it

you can email on start, success or failure

you can control w2ho can change or run the job. you can change ownershiop of one user. this type of stuff is pretty standard if you are used to that.

once the jobs are runnign and have run in the past, you can acces them through the runs tab. it has active and completed data for jobs. you can clidk into an active job for reatime visualizations of execution.

if yuou run a delta live tables pipeline wihtin a job, the results won't show in the job results window, but you get a link to go back to the detla live tables section of databricks where you can view them.

so all in all what you did was:

- crfeate a delta live tables declarative pipoeline to stream data from sources that were autoloaded in from json or parquet files in dbfs somewhere.
- create a job where you - first positioned the source data for ingest - then ran the entire DLT pipeline - then ran a notebook that performed additoinal queries againts the gold table that was released.
  I shoudl probably try do do this kind of thing on my own with them, seems like a good itea.

  one powerful feature of jobs is that you can choose to repair a run with only the tasks that failed during your last run. you can select exactly which task to start with within a run.

  seems like for a pipieline you have to remember to terminate the cluster.

  ## databricks sql

for one, the workspace that we typcially used in databricks is the data science and engineering workspace. you can change to SQL by using the 'sql persona' avaiable from a drop down somewhere in the top left of databricks interface

databgricks SQL or dbsql, is a data warehouse that scales well and let's you run all tables with a unified governance model

SQL warehouse - this is the compute power provided to databricks sql. it's a sql engine based on a spark cluster.

setup is pretty standard, their verison is old but the premise is still the same, I would create a dedicated cluster or a serverless cluster and ther is pro and classic. for mine the standard 4 vCPUs available on the free trial were not sufficent for the smallest compute size by a factor of 4 so I don't get to play along I have to watch.

once you have a warehouse ready to use, you can go get to some data. dashboards, visit gallery, NY taxi eda is there. you could also create yoiur own new dashboard from scratch, that is kind of the point eventually.

## dashboards

you can refresh anytime. you can view the query for any visualization with three dots in cornner

navigating in the dashboard, you can edit the visualizaitons tehre are a lot of tweaks you know

you can add visualizations with the ` +` symbol.

you can name the visualizations

once you make a new visualization it is not inherently from the notebook in your dashboard. you habve to add it

you can edit the visualization after it is added to resize it and such

dashboards can be shared with other users . you have the option to run them as if they were the owner or viewer.
if you don't own the data that is the basis for the dashboard loaded as the users and have it in your workspace, then the other option seems better, run as owner.

there is a sql editor for the sql warehouse you connect to and then the sql editor interface supports querying against the tables in this warehouse

f8un trick in sql editor, if you want to ad the tablename to a query, you can click on the >> button by that table name int he schema browser panel on right. this works for columns too.

you can save a query and give it a name and then select three dots on query tab to add the query to the sample dashboard. there is a three dots down at the bottom by table

you can schedule the refresh of the dashboard for every time period interval.

there is also a queries sidebar option that shows you your queries.

you can use queries to set up alerts also. there is an alerts side menu option also. you can give the alert a name. you can set an alert trigger like "total_fare > 10000 " . you can set up the notification to receive when the trigger happens.

## data object privileges and data governance model

the governance model let's users manage access controls with grant, deny and revoke operatyions. this is programmatic and it applies to the data objects.

syntax for grants: `grant <privilege> on <object> <object name> to <user or group>`

example: `grant select on table my_table to user@123`

what types of data objects are there?

catalog
schema (database)
table
view
function
any file

then there are the types of permissions you can grant:

select
modify
create
read_metadata
usage
all privileges

who can grant?

database admin - all catalog and filesystem grant privileges
catalog owner - can grant on anythign inthe catalog
database owner - can grant on anything in the database
table owner - can grant on anythign in that table
view owner - ""
function owner " . "

these didn't go over it but you can also deny or revoke privileges to users with these roles at the right scope and you can also show grants to see what people have for that object

very important once you ahve somthing like a table that you want ot configure permissions on, that in addition to select or modify or whatever you also grant usage permissions or users won't be able to do anything.

## data explorer to manage permissions

data explorer let's users navigate different objects, and they enable users to set permiossions

when on a db in the data explorer, use the permissions tab to suss out what is wrong.

UI is conveneint, you ahve things like a checkbox and revoke button, and you can edit owner with a button as well. turns out in the UI you can set the owner to an individual or a group
all the options are the dame as teh adata governance framework in the code, just has a gui in front of it.

only thing different is the you can't use the 'any file' option, you ahve to use sql

you can look at the sql history in the left hand panel to look at teh query history run behind the scenes for the data explorer.

## Unity Catalog

what is it?

governance solution for data.
one place, in the center, one stop shop
you can store your data here even if you are using it in azure, aws and gcp, just one time for databricks.

hyou can do governance3 with sql, you can do it for all different kinds of data objects: files, machine learning models, tables, dashboards

this is about data access rules, write once run anywhere solution for that. pretty slick. I can control the access to my data centrally and I mean really centrally

two aspects of it, user/group management was at the workspace level, and then access was managed at the hive metastore level

in unity catalog, this stils outside the workspace and is accessed with a UI called the account console

both the user management and the unity catalog metastore are outside of the workspace and accessed with this account console where they get assigned to workspaces. one metastore can be assigned to multiple workspaces, so dbfs storage and ACLs are shared. ACLs are4 access control lists.

3 level namespace?

so the databricks namespacing is familiar now, the schema is the database it belongs to and you have a decent mental model of what that looks like. all that the unity catalog does is add another namespace one level up. but the structure goes one level up from that it goes:

Unity Catalog metastore - top level area, stores metadata about the objects being controlled by the metastore as well as acess control lists for access to those object

the unity catalog metastore contains the catalog, and that is the highest level namespace for referring to tables.

the default for databricks is still hive metastore, but the unity catalog metastore as improvementsfrom e security standpoint and is preferred for environments where this is important

you can't have too many catalogs

security model

unity catalog supports storage credentials

there is stuff for delta sharing but it is out of scope

theere are only three thypes of identities to manage in unity catalog: users, service principals, and groups. that is pretty easy. service principals are systems, the other two are either one or plural

groups are more cdomplicated than I thought they can mix people and service principals and be nested.

unity catalog manages identities with identity federation, which means that it can create an identity at the unity catalog levela nd then that propagates to teh workspaces, rather than managing and creating redundant copies of an identity per workspace

UC privileges:

create
usage
modify
select

read files
write files -- the read and write files together are the replacement for hive metastore's any file option

execute - this is for controlling access to running udf

grant model similar to the data governance one for hive metastore, but you have more privilege types, you have these securable objects that are defined, and you have defined principals

UC is addative, so you can keep using legacy hive metastore.

you can bypass unity catalog with hive_metastore, which will always go with the underlying metastore that is attached to their db

UC benefits
-centralized data governance that is the big one

- built in data exploration
- automatic data lineage

- you don't have to migrate to it because it is addative

https://accounts.cloud.databricks.com
this is haw to log yourself out and go be an account admin to do things at the root level

Gaps I'm hitting second time around:

- syntax for some things, like how to use the %fs command. ls '', and then there is head '' for viewing files
- describe detail vs. describe history vs. expanded detail they are all good and I rememberd them but maybe not same names
- remembering what delta tables can do and how they do it.
  - I remembered that delta tables were storing metadata in the hive metastore, needed to remember dbfs:/user/hive/warehouse is the default location
  - that 'managed' table is the same as delta table and 'external' is the name for not managed.
  - that 'using delta' is the default and
  - that if you do 'using' for something other than delta, you are creating an external table and the consequences of this are that you sacrifice all of that restore and optimize capability that delta tables have. examples of this could be using jdbc or using csv, this leaves the data in external tables and doesn't copy them into parquet files.
  - that for time travel queries the syntax is `select * from table version as of <version>` or `timestamp as of <timestamp>` or `@v<version>`
  - that zorder indexing is part of the optimize command, it is a subcommand.
    - I learned the new thing that optimize is idempotent but zorder indexing is not. I also learned that zorder indexign is meant ot be incremental
    - I need to think a bit to remember what zorder indexing is all about. if optimize is to use fewer files to represent the data to save on performance, zorder indexin is more about partitioning the data so that things that should be logically grouped in the files and will be retrieved together are grouped that way for faster reads. realliy understanding how this provideds a benefit: it is like a; hashtable, it reorders the specified colums so that there are bins in the files and it knows where to look, it is like indexing so that it can always find the things in the box, rather than searching from bin to bin. very much like alphabetically ordering nametags when you come into an event so that you just look for the letter that corresponds to your name.
- I did remember vacuum and my mental model of delta tables was strong enough to remember the implications of vacuuming a delta table and then trying to time travel back to a version that was vacuumed
  remember you can set a retention period in the vacuum command `vacuum <table name> <reterntion period>`
- going over the comments syntax I got that eretained
- partitioning using one or more columns for performance reasons with `partitioned by` is somethign I knew. most use cases not benefitting from it and even being harmed by it is somethign I missed first time around, it is becaseu of the small file issue with the way databricks stores something.
- create tabel vs ctas - don't need a schema in fact can't have one because it is automatically inferred. table is empty and you need an insert statement
- ctas vs create table again, you use ctas you get data because you are creating it out of a select statement.
- forgot there were both not null and check constraints. no data violating constraint already in table
- constraint for check uses `check` keywoard. I'm guessing not null uses `not null` and has now conditional clause
- syntax for cloning `create table <table> deep clone <source_table>` shallow is same but shallow
- one difference delta vs csv and other is that delta makes sure you are always querying agasint the latest source data for your tables.
- refreshing data in a table invalidates the cache which can meant reading all files again which takes a long time, one reason you don't want ot have to manually tell databricks to refresh a table that is external and not delta
- ctas can import from externally defined resources with defined schemas
- csv doesn't have defined schema, so what to do? if you try to use CTAS, the parsing will be bad
- the solution with things like csv is that you can use create temp view with an explicit schema and with using csv, which creates the schema you want but you still have a non delta external table, but then you can use the ctas statement with a select from the temp view to infer the schema from the temp view and set up a managed table.
- overwriting tablers is bette than dropping and recreating for ao bunch of reasons. it is acid so concurrent read and overwrite is possible without data loss, you save time on recursive directory listing or file deletion while it drops the tables, it is append only, you also don't lose the table, you get to go back tot he old one if you want through time travel
- I feel liek this si one I'm going to get tested on. `create or replace table as ` is one that will overwrite but also create, `insert override` will just overwrite. also the former will allow schema changes if the inferred schema from the select is different that original schema.
- important, insert into vs merge, you upsert into the target table from view or table. can add new, update records
- for merge into you don't always have to specify the when matched and when not matched, so you can just to inserts or just do updates or both.
- for merge into you can use temporary views as well as views and tables pretty muc hanything
- things to remember about advanced queries with spark
  - spark can doi nested json queries easily with ':' delimiter so for a column in the query, colons to drill down into the json object
  - spark can also create a struct out of json column. you can do this with from_json() but you also need a sample of the schema, which you can get just by getting one row of the column as an example so that spark can parse it.
  - so the real thing is from_json(column_name, schema_of_json())
  - when you parse json with advanced spark sql, you have : to drill into json during select, you ahve .\* to flatten json to columns, and you have explode(array) to make a row for every element in an array column. you also have collect_set() to remove duplicates from arrays, and we have the array_distinct which we can apply outside of flatten(collect_set()) which would keep only distinct values. so you collect_set first to get rid of dupes in the inner arrays, then you flatten to a single l ong array, then you use array_distinct to just get the values from that.
  - learning about advancecd spark sql stuff
    - complex types with higher order functions
    - filter function
    - transform function
    - udfs, adn you can drop them and they have case when statements
- spark structured streaming
  - one I got wrong for this before, once=True isn't as good as availableNow=True because once=True does a single batch
  - separate chekcpointLocation is required for every streaming write to ensure processwing integrity
  - structured streaming is exactly once and therefore idempotent. this only works if the source is reapeatable
  - remember you can't sort or dedup w2ith streaming (probably because this involves comparing incoming streamed data with data that hasn't abeen streamed or has already been streamed. ) windowing and watermarking can help with this
  - trigger\*() method in use, medallion or multi hop archtiecture, seems like creating temporary view in spark sql aor spark api is how you do it and then nothing happens unless you try to look at or write data with a future query. so, autoloader for initial ingest, then spark readStream for each future hop because the prior ttep would have left us with a table that we can use as a source that is a delta table. then you have some sql command in spark to make a temp view that represents the tranformation form one layer to another, and then you use spark writeStream to write it to a persistent source. structured streaming cannot be done on a table if they receive overwrites from upstream.
  - remember to rerun tables that are batch jobs after you add data, doesn't work like streaming.
    [
