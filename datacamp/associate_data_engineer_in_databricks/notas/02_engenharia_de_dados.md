# Engenharia de Dados — Fundamentos

## Fluxo de trabalho de dados
coleta e armazenamento (engenheiro de dados) -> preparacao -> exploracao e visualizacao -> experimentacao e predicao

- engenheiro de dados: dar entrada nos dados, otimizar banco de dados, arquitetura de dados
- big data: dados grandes, saber lidar com seu tamanho
- engenheiro precisa dos 5 v (volume, variedade, velocidade, veracidade, valor)

## Diferença entre engenheiro x cientista
- engenheiro: faz a primeira acao, coleta e armazena (realiza a base)
- cientista: explora, predicao, visualizacao
- como engenheiros viabilizam o processo: gerenciam entrega e armazenamento dos dados, mantem bancos otimizados, pipelines de dados
- cientistas precisam acessar tabelas para explorar e analisar dados, usam saidas de pipelines para usar dados

## Pipelines de dados
(dados o novo petroleo mundial - riqueza) - movimentam dados de um lugar para outro

empresas recebem dados de varias fontes, pipelines automatiza essa locomoção de dados entre plataformas, para que os cientistas possam ter dados atualizados

fontes de dados extraidos (mobile, desktop, site, sistemas internos) que vao para DATA LAKE -- depois banco de dados entre tabelas ---> todas essas direcoes dos dados, são pipelines (garantem fluxo eficiente de trabalho das proximas etapas)

**ETL (Extract Transform Load)**

## Tipos de dados
- dados estruturados - rigidos (organizados em linhas e colunas)
- dados semi-estruturados - mais liberdade (nosql, json) - tem estrutura mas nem sempre são seguidos os schemas rigidamente
- dados não estruturados - não seguem modelo, nao cabem em linhas, geralmente midia, geralmente armazenados em data lake ou data warehouse (foto, audio, pdf...)

rdbms = Sistema de gerenciamento de banco de dados relacional

## Data Lake x Data Warehouse
**data lake** = lugar de armazenamento de todos os dados, estão brutos, não organizados (muito grande), armazena todo o tipo de dados (estruturado, semi, e não), mais barato, dificil de analisar, usado para big data em tempo real, usado por cientista de dados. Catalogo de dados (de onde vem, para o que são usados, quem é dono, garante reprodutibilidade, boa solução)

**data warehouse** = lugar de armazenamento de dados especificos para uso especificos (menor), armazena somente dados estruturados, mais caro, mais otimizado para analise de dados, usado por analista de dados e negocio. Tipo de banco de dados

## Processar dados
(dados brutos) -> informações valiosas
- otimizar custos de armazenamento
- tarefas de manipulação, organizacao, limpeza de dados, decisões de status de arquivos e informações

## Agendamento
- pode ser aplicado a qualquer tarefa listada no processamento de dados
- o agendamento mantem o sistema coeso
- mantem cada parte no lugar e organiza seu funcionamento conjunto
- executa tarefas em uma ordem especifica e resolve todas as dependencias
- pode ser manualmente, por horário e por sensor
- exemplos: atualizar banco de dados toda sexta (horario), sensor (trigger, se adicionar um user atualizar)
- ferramenta: apache airflow

## Entrada dos dados
- pode ser em lotes e fluxos
- lotes: agrupam registros em intervalos, mais economico
- fluxos: envio de registros individuais imediatamente

## Processamento / Computação Paralela
- em memoria, processamento mais potente, quase toda plataforma de processamento de bigdata usa
- divisão de tarefa em cluster (varios computadores) com subtarefas menores
- capacidade de processamento
- ao inves de carregar todos os dados na memoria de um unico pc, carrega um pouco em cada pc
- desvantagens: movimentação de dados

## Computação em nuvem para processamento de dados
- evita desperdicio de custos de funcionamento e manutenção
- banco de dados muito importante na nuvem (confiavel, disponibilidade)

### Recursos mais utilizados de cada nuvem
- aws: s3, ec2, rds
- microsoft azure: azure blob storage, vm azure, sql azure
- google cloud: google cloud storage, google compute engine, google cloud sql

pode montar o serviço de engenharia de dados em MULTINUVEM (menos dependencia de um unico fornecedor, custo beneficio)
