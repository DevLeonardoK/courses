# Delta Lake e Ingestão de Dados

## Formato Delta
formato delta (lakehouse), muito usado - formato de armazenamento open-source, conjunto de tabelas parquet, log de transacoes em json, compativel com ACID (atomicity, consistency, isolation, durability), suporta batch e streaming

uma tabela é como se fosse uma pasta no data lake:

```
s3://empresa/silver/clientes/
├── part-0001.parquet
├── part-0002.parquet
├── part-0003.parquet
└── _delta_log/
```

o spark le todos os arquivos, ai que entram optimize e zorder

## Ingesting data
- lakeflow connect - connection builtin with database and saas TO --> delta lake (cria pipelines automaticamente)
- data upload (csv, parquet e tal) --> delta lake
- copy into -> copiar dados de object storage cloud into delta table, better for static
  ```sql
  copy into my_table FROM 'path' fileformat = parquet, format_options, copy_options
  ```
- auto loader (automaticamente ingest novos dados from cloud storage, melhor para bancos grandes e que mudam constantemente)
  ```sql
  create table customers as select * from cloud_files("path to files")
  ```
  bom para sistemas que precisam de dados em tempo real

possivel criar uma tabela a partir dos dados ja existentes no data ingest

## Data engineer advanced patterns
appending data x cdc (change data capture):
- appending - so adiciona sem pesquisar se ja existe
- capture (cdc) - atualiza o registro se houver, caso contrario faz insert

## Otimização
- optimize = comando do delta lake para compactar arquivos menores em arquivos maiores, geralmente combinado com o zorder para relacionar dados fisicos mais proximos e acelerar filtros em colunas especificas
- partitioned by (ano) - cria subpastas por ano, usado quando a coluna é muito usada nos filtros
- partition é low cardinality / zorder é high cardinality

## Tabelas Managed x Unmanaged
- **Unmanaged**: criada com `LOCATION`, aponta para storage externo — Databricks só referencia, não gerencia os dados
- **Managed**: criada sem `LOCATION` — Databricks armazena fisicamente e é responsável pelos dados
- `USING DELTA` = usar formato Delta Lake (não é banco, é formato de armazenamento); uma tabela delta é uma pasta com vários arquivos parquet + `_delta_log/`
- `LOCATION` sobrescreve o storage padrão do metastore

## Views
- `CREATE VIEW` / `CREATE OR REPLACE VIEW` — útil para consultas muito reutilizadas
- `CREATE OR REPLACE TEMP VIEW` — existe apenas durante a sessão atual

## PII (Personally Identifiable Information)
Informação Pessoal Identificável — dados que identificam uma pessoa:
- Nome completo
- CPF, RG, Passaporte, CNH
- E-mail pessoal
- Telefone
