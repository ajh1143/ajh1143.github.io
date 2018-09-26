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
```Python3
query = "FROM table SELECT *"
```

## Requesting a Query
```Python3
table_query = spark.sql(query)
```

## Query Results

```Python3
table_query.show()
```

# Create DataFrames

## Convert Query Results to a DataFrame
```Python3
df = table_query.toPandas()
```

# Create Clusters

## Convert DataFrame to a Spark Cluster
```Python3
spark_df = spark.createDataFrame(df)
```

# Tables

## Create temporary table
```Python3
spark_df.createOrReplaceTempView("temp")
```

## Creating a New Table
```Python3
table = spark.table("title")
```

## Add a New Column
```Python3
table = table.withColumn("new_Column", table.oldColumn + 1)
```
## Viewing Available Tables

```Python3
print(spark.catalog.listTables())
```

# CSV Files 

## Convert CSV file to Spark Cluster
```Python3
file_path = "filepath//filename.csv"
```

## Read the File Data
```Python3
fileContents = spark.read.csv(file_path, header=True)
```

## Display The Data
```Python3
fileContents.show()
```

