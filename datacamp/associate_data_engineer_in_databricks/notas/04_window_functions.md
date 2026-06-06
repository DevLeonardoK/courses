# Window Functions (Funções de Janela)

usado para usar calculos agregados sem usar no group by

sao funcoes que realizam calculos sobre conjunto de linhas, sem agrupar nem reduzir o numero de linhas

```sql
avg(........) over() alias .....
rank() over(order by coluna desc) alias
```

quando tenho uma agregação e depois uma window function e depois group by, não preciso de over na agregacao

## Partition by
particao de filtro/agregacoes/janelas por colunas - divide dados em grupos

```sql
over(partition by ......)
```

## Sliding windows
usado para calcular metricas em um conjunto de linhas vizinhas

- preceding - antes da linha atual (current row)
- following - apos linha atual (current row)
- unbounded preceding - todas as linhas desde o comeco
- unbounded following - todas as linhas desde o final
- current row - significa que quer encerrar o codigo na linha atual

| dia | vendas |
| --- | ------ |
| 1   | 10     |
| 2   | 20     |
| 3   | 30     |
| 4   | 40     |
| 5   | 50     |

```sql
SELECT
    dia,
    vendas,
    AVG(vendas) OVER (
        ORDER BY dia
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS media_3_dias
FROM vendas;
```

| dia | vendas | media_3_dias |
| --- | ------ | ------------ |
| 1   | 10     | 10           |
| 2   | 20     | 15           |
| 3   | 30     | 20           |
| 4   | 40     | 30           |
| 5   | 50     | 40           |

pode ser utilizado valores current row como inicio:

```sql
SELECT
    -- Select the date and away goals
    date,
    away_goal,
    -- Create a running total sum and running average of away goals
    sum(away_goal) over(ORDER BY date DESC
         ROWS BETWEEN current row AND unbounded following) AS running_total,
    avg(away_goal) over(ORDER BY date DESC
         ROWS BETWEEN current row AND unbounded following) AS running_avg
FROM match
WHERE
	awayteam_id = 9908
    AND season = '2011/2012';
```

## Lag e Lead
lag e lead sao window functions para acessar valores das linhas anteriores e posteriores:

```sql
-- anterior
SELECT
    mes,
    vendas,
    LAG(vendas) OVER (
        ORDER BY mes
    ) AS vendas_mes_anterior
FROM vendas;

-- posterior
SELECT
    mes,
    vendas,
    LEAD(vendas) OVER (
        ORDER BY mes
    ) AS vendas_proximo_mes
FROM vendas;
```
