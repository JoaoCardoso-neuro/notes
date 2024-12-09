---
tags:
  - ddos
  - machinelearning
aliases:
  - Apache Spark
  - PySpark
---

---
## Conceito

Spark é uma plataforma para computação em cluster, nela pode-se dividir os dados em nodes para realização de computação paralela (processar os dados em cada node separadamente) para efetuar a conexão com o cluster utiliza-se o objeto *SparkContext* e *SparkSession* para a interface com a conexão

## Comandos Importantes

### Criando uma Interface (*SparkSession*)

``` python
# Import SparkSession from pyspark.sql

from pyspark.sql import SparkSession as ss

# Create my_spark

my_spark = ss.builder.getOrCreate()

# Print my_spark

print(my_spark)
```

## Verificando Tabelas

O atributo *catalog* do objeto *spark* lista todos os dados do cluster, e o método *.listTables()* mostra os nomes das tabelas

``` python
# Print the tables in the catalog

print(spark.catalog.listTables())
```

### Queries

No spark podemos realizar queries do SQL usando o método *.sql()*

``` python
query = "FROM flights SELECT * LIMIT 10"

# Get the first 10 rows of flights
flights10 = spark.sql(query)

# Show the results
flights10.show()

```

Para converter uma query em um dataframe do pandas utilizar o método *.toPandas()*

``` python
query = "SELECT origin, dest, COUNT(*) as N FROM flights GROUP BY origin, dest"

# Run the query
flight_counts = spark.sql(query)

# Convert the results to a pandas DataFrame
pd_counts = flight_counts.toPandas()

# Print the head of pd_counts
print(pd_counts.head())
```

## Criando DataFrames

Para criar um dataframe no Spark a partir de um do pandas utilizar *.createDataFrame()* para tabela local e *.createTempView()* 