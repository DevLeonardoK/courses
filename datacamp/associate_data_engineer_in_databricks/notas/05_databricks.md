# Databricks

## Nascimento do Lakehouse
data warehouse muito bom para estruturados porem é pouco flexivel, data lake é flexivel mas nao organizado.
surgiu entao o lakehouse - mistura de data lake com data warehouse, flexibilidade e simplicidade

data lakes offer flexibility and low cost but lack reliability. Data warehouses deliver performance and governance but at higher cost and less flexibility. The lakehouse combines both into a single platform, powered by delta lake for reliability, ACID transactions for consistency and unity catalog for governance

- databricks tem data intelligence (ia integrada, desenvolvimento para ia e bi)
- databricks é multicloud suporte
- pode trabalhar com python, sql, r, scala; databricks foi baseado no apache spark (processamento em memoria, clusters)

- catalogs - unity catalogs, todos os dados
- compute - clusters / processamento

## Arquitetura do Databricks
mecanismo de escala - lakehouse

databricks platform:
- control plane = databricks managed (ui, scheduling, management)
- data plane = your cloud (compute, storage, data)
- audit logs (stored as system tables in your account)
- your data never leaves your cloud environment

## Administração
- admin - supervisiona tudo, deve garantir acesso workspace e outros
- workspace admin - gerente do setor = garantir acesso workspace e recursos necessarios para entregar resultados
- databricks marketplace - conjunto de dados de terceiros
- partner connect - conexoes via ui, tecnologias parceiras, conexoes de bi, ferramentas de ingestao

importancia da gestao dos dados: protecao e seguranca, confianca, profissionalismo

## Acesso aos dados
depois de armazenar os dados, precisamos decidir como acessar; databricks usa o unity catalog (grant, revoke) acesso granular aos dados para o usuario

dbfs (databricks file storage)

## Clusters
tipos de cluster:
- classico (recurso compute vm, compute plane)
- serverless (da acesso aos usuarios do catalog explorer, inicio rapido, mas menos controle)

single node vs multi-node (todos vao ter instalado o databricks runtime - versao otimizada do apache spark, photon para sql mais rapido):
- single: cluster com apenas um driver node, ainda roda spark, tambem frameworks single-node (pandas), otimo para datasets menores (barato)
- multi: um driver node (cerebro) e um ou mais worker nodes (spark distribui)

jobs - single task cluster
databricks runtime - base do sistema

- pode ter varios tipos de cluster: meus proprios, compartilhados e todos os clusters
- cluster estados: pending, running, restarting, terminating, terminated
- autoscaling: add ou remove workers based on demand
- cluster policies - controla casos de incidentes
- cluster terminated = settings mantem, porem dados in memory se perdem

## Notebooks
| Magic | Função |
| ----- | ------ |
| %python | Run Python code |
| %sql | Run SQL queries |
| %scala | Run Scala code |
| %r | Run R code |
| %md | Render Markdown |
| %sh | Run shell commands |
| %run | executes another notebook in the same context (loads functions from other notebook into your session) |

notebook sharing - permissoes | versionamento com alguma ferramenta como github/gitlab

## Análise de dados (muito importante e relevante para empresas)
sql in databricks intelligence platform

data warehouses - great for sql workloads
- typically expensive
- limited capabilities and integrations

data lakes
- great for non sql workloads
- cost effective
- open source technologies
- sem limitacoes

## Governance - Unity Catalog
- metastore - one per account, top level
- catalogs - dev ou prod
- schemas - desenvolvimento | support
- contains tables, views, functions

- access control every level (grants)
- data lineage

## Delta Sharing
two different ways:
- native: databricks unity catalog to databricks unity catalog
- open protocol: databricks to any platform: spark, pandas, power bi, snowflake

custos:
- same region - free
- cross region but same cloud = egress charges for data transfer
- cross cloud - highest fees (azure to aws)

if both organizacoes estao no databricks entao deve ser feito databricks native sharing

## Lakehouse Federation
| Critério | Federation | Batch copy |
| -------- | ---------- | ---------- |
| Access | Real-time | Batch copy |
| Query volume | Low | High |
| Latency | Source-dependent | Low |
| Compliance | No copies needed | Data moves |
| Transforms | Limited | Full medallion |

## Deployment and next steps
dab - databricks automated deployment (Databricks Asset Bundles)
