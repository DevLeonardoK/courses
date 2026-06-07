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

## Spark Catalog
API para interagir com o metastore do Spark (tabelas, views, cache)
```python
spark.catalog.listTables()
spark.catalog.cacheTable('table1')
spark.catalog.isCached('table1')
spark.catalog.uncacheTable('table1')
```

## Logging
```python
logging.debug("text_df columns: %s", text_df.columns)
logging.info("table1 is cached: %s", spark.catalog.isCached(tableName="table1"))
logging.warning("The first row of text_df:\n %s", text_df.first())
logging.error("Selected columns: %s", text_df.select("id", "word"))
```
- `debug` / `info` — não disparam ação no dataframe (lazy)
- `warning` / `error` com `.first()` ou `.collect()` — disparam execução real

## Transformações de Dados (Spark SQL / PySpark)
```python
# filtro com startswith
df.filter(df["coluna"].startswith("A"))

# preencher nulos
df_clean = df_clean.na.fill({"Description": "Unknown", "UnitPrice": 0.0})

# remover duplicatas por subconjunto de colunas
df_clean = df_clean.dropDuplicates(subset=["InvoiceNo", "StockCode", "InvoiceDate"])
```

## Broadcast Join (detalhado)
- O problema do join padrão é o **shuffle**: os dados são embaralhados pela rede para serem agrupados, o que é lento
- **Broadcast join**: copia a tabela menor para cada executor — o join ocorre localmente, sem tráfego de rede
- Não funciona com tabelas grandes (memória do executor seria insuficiente)
- O Spark faz **auto broadcast join** automaticamente quando detecta que uma tabela é pequena o suficiente
- Verificar no `explain()` se foi usado: aparece como `BroadcastHashJoin`

## DLT (Delta Live Tables)
```python
@dlt.table(name="bronze")
```
- Decorator usado para definir tabelas em pipelines DLT — o Spark gerencia dependências e execução automaticamente