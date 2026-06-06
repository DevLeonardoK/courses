# SQL Básico

Database = Conjunto de tabelas, linhas e colunas
- rows = dados individuais, conjunto de informações
- columns = atributos / propriedades

sql = usado para retornar dados - comunicação com banco de dados

## Tabela
- nome em minusculo e separado por _
- nome simples e referenciar dados
- nome de coluna no singular

## Tipos de dados
- float e numeric pode armazenar numeros (numeric ate 38 casas decimais antes e depois)

## Views
- views (consulta sql) não salva dados

```sql
create view employee_view as select id, name, year_hired from employees;
```

## Tipos de versões
variantes de sql devem seguir um padrao (iso)
- postgresql = free, open-source, patrocinado por darpa
- sqlserver = free e pago, criado pela microsoft, usa t-sql
- diferenças: sintax (limit x top) = limitar resultados
