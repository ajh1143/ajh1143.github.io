---
layout: post
title: "PySpark"
---
<img src="/Images/PySpark/PySpark_title.jpg" class="inline"/><br>
It's Electric!

# What is PySpark?
PySpark exposes the Apache Spark programming model to Python through a feature rich API. Utilize the ease of python scripting for your 
next parallel computing cluster task in machine learning, SQL, graph analytics and streaming.

# What is cluster computing?
Method for parallel computing, where large data is parsed into smaller pieces, and processed in cluster nodes. 
Cluster nodes are slaves controlled by a master, which delegates data delivery and reception after processing.

# Why is it useful?
It's an optimized solution for very large data sets and processes that are too large and computationally expensive for a single machine or small set up.

## Getting Started
How do we connect to a cluster? We create an instance of SparkContext, `sc = SparkContext()`

Then we can do `spark = sc.SparkSession()` and make calls through spark

To start working with Spark DataFrames, you first have to create a SparkSession object from your SparkContext. You
can think of the SparkContext as your connection to the cluster and the SparkSession as your interface with that connection.

# Querying Data

## Building Queries

Construct a query as a string using standard SQL syntax, save as a `query` variable for convenience.
```Python3
query = "FROM table SELECT *"
```

## Requesting a Query
Pass the query to `spark.sql()` and save the results.

```Python3
table_query = spark.sql(query)
```

## Viewing Query Results
Append `.show()` to your requested query to view your instantiated table.

```Python3
table_query.show()
```

# Create DataFrames

## Convert Query Results to a DataFrame
Append `.toPandas()` to a query result to convert format to a Pandas DataFrame.

```Python3
df = table_query.toPandas()
```

# Clusters

## Convert DataFrame to a Spark Cluster
Pass a dataframe into `spark.createDataFrame()` as an argument to generate a Spark Cluster from your initial DataFrame.

```Python3
spark_df = spark.createDataFrame(df)
```

# Tables

## Create temporary table 
To initialize a temporary table, chain `.createOrReplaceTempView("title")` to a Spark Cluster DatFrame

```Python3
spark_df.createOrReplaceTempView("temp")
```

## Creating a New Table
Generate a new table by simply calling the `.table()` module from the Spark library

```Python3
table = spark.table("title")
```

## Add a New Column
You can add a new column to an existing table with two parameters defining the new column's name, and a series of data as shown below.

```Python3
table = table.withColumn("new_Column", table.oldColumn + 1)
```
## Viewing Available Tables
You can take a peek at the tables you have available with the `.listTables()` feature.

```Python3
print(spark.catalog.listTables())
```

# Convert CSV file to Spark Cluster

## Set Target File
Create a string with the location and name of your file.

```Python3
file_path = "filepath//filename.csv"
```

## Read the File Data
Pass the file path to `.read.csv()` with an optional parameter to use headers from the CSV file.

```Python3
fileContents = spark.read.csv(file_path, header=True)
```

## Display The Data
View your data by using `.show()`

```Python3
fileContents.show()
```

