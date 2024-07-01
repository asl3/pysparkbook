# PySpark Basics

## Build a Spark Session

First, we need a SparkSession to perform operations with Spark.

Here is how to start a SparkSession:

```
from pyspark.sql import SparkSession

spark = SparkSession.builder.getOrCreate()
```

## The pyspark shell

Spark’s shell provides a simple way to learn the API, 
as well as a powerful tool to analyze data interactively. 

To start the pyspark shell, simply running the following terminal command 
in the Spark directory:

```commandline
>>> pyspark
```

You should see something like this:

```commandline
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /__ / .__/\_,_/_/ /_/\_\   version 3.5.0
      /_/


```

Now we can run pyspark code directly from the shell command line,
for quick iteration when testing our code.

## DataFrames

A DataFrame is a two-dimensional labeled data structure with columns 
of potentially different types. 

You can think of a DataFrame like a spreadsheet, a SQL table, or a dictionary of series objects. 
Apache Spark DataFrames provide a rich set of APIs (select columns, filter, join, aggregate, etc.) 
that allow you to solve common data analysis problems efficiently.

Apache Spark DataFrames are an abstraction built on top of Resilient Distributed Datasets (RDDs).
Direct use of RDDs are deprecated as of Spark 4.0, with the release of Spark Connect.
Interacting directly with Spark DataFrames uses a unified planning and optimization engine, 
allowing us to get nearly identical performance across all supported languages on Databricks (Python, SQL, Scala, and R).

### Create a DataFrame

Here's how to create a simple DataFrame:

```commandline
employees = [{"name": "John D.", "age": 30},
  {"name": "Alice G.", "age": 25},
  {"name": "Bob T.", "age": 35},
  {"name": "Eve A.", "age": 28}]

df = spark.createDataFrame(employees)
```

We can use PySpark to view and interact with our DataFrame:

### Print the DataFrame schema

```commandline
df.printSchema()
```

```
root
 |-- age: long (nullable = true)
 |-- name: string (nullable = true)
```

### Rename columns

```commandline
df2 = df_csv.withColumnRenamed("name", "full_name")
df2.printSchema
```

```
root
 |-- age: long (nullable = true)
 |-- full_name: string (nullable = true)
```

### Filter rows

We can filter for employees within a certain age range.
The following `df.filter` will display a DataFrame with rows that match our age condition:

```
display(df.filter(df["age"] > 26 and df["age"] < 32))
```

We can also use `df.where` to get the same result:
```
display(df.where(df["age"] > 26 and df["age"] < 32))
```