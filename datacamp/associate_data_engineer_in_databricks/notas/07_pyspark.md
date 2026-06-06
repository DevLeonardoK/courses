# PySpark

## Básico
```python
spark.read.csv(path, header, inferSchema)
```
- `.show()` - 5 primeiras linhas
- `.count()` - contagem
- `.select()` - seleciona colunas
- `.filter()` - filtra linhas
- `.groupBy()` - agrupa linhas
- `.agg()` - agrega valores

## Construção de um schema para dataframe
```python
schema = StructType([
    StructField("id", IntegerType(), True),  # True = nullable
    StructField("name", StringType(), False)
])
```

## Joins no pyspark
```python
df_joined = df1.join(df2, on="id", how="inner")

df_joined = df1.join(df2, df1.id == df2.name, how="inner")
```

## Unions
```python
df_union = df1.union(df2)
```

## Struct type
```python
df = df.withColumn(
    "name_struct",
    struct("first_name", "last_name")
)
# ==== {Leonardo, Kremer}
```

## UDF (Função definida pelo usuário / função personalizada)
- udf pandas para dados maiores
- udf spark para dados menores

```python
from pyspark.sql.functions import pandas_udf

@pandas_udf(data_type)
def minha_funcao(...):
    ...
```

## RDDs (Conjunto de dados distribuídos resilientes)
Coleção de dados distribuidos em um cluster com recuperação automatica de falhas de nós
- rdds sao imutaveis
- `.rdd` cria
- sem schema
- nao muito otimizado
- `.map` - aplica funcoes
- `.collect` - coleta dados do cluster - mas ele é pesado

## Spark SQL
poderoso pois usa sql e cluster do spark
muito bem integrado com pyspark e sql

## PySpark em escala
a medida que os dados crescem devemos otimizar para bom funcionamento das pipelines
- metodos como broadcast (carregar conjuntos de pequenos dados em todos os clusters, usado no JOIN)
- `.cache` - guarda dataframe na memoria para consulta rapida do dataframe
- `.persist` - guarda na memoria e no disk / `.unpersist` = caso nao caiba na memoria, usa o disco
- preferir `.map` do que `.groupby`, pois é melhor, mais leve em grande escala
- usar broadcast em join (usa todo o processamento mesmo em datasets menores)

## NumPy (extra)
numpy = numeric python, trabalhar com matrizes como se fosse valor unico, possui tipo unico
- 2d = linha x coluna
