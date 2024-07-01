# Data Loading

[TODO: improve the examples, test the code]

There are several ways we can load data in PySpark.

## Load local file into a DataFrame

PySpark provides APIs to load data from file formats like CSV, parquet, JSON, etc.
For a detailed description of which APIs fit your use case, please refer to 
the [PySpark docs](https://spark.apache.org/docs/latest/sql-data-sources-load-save-functions.html).

Here is an example of how to ingest data from a local CSV file to a DataFrame:

```commandline
df_csv = spark.read.csv(f"{path_volume}/{file_name}",
    header=True,
    inferSchema=True,
    sep=",")
display(df_csv)
```

## Run SQL on Files Directly

We can also query a file directly with SQL:

```commandline
df = spark.sql("SELECT * FROM parquet.`examples/src/main/resources/users.parquet`")
```




