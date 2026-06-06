# SQL Intermediário — Combinação de dados, Joins e CTE

## Combinação de dados
- verticalmente: union (rows de mesma estrutura)
- horizontalmente: tabelas (joins)

### Union
- union tambem chamado de stacking ou appending
- union distinct - uniao dos dados mas deixando de fora os duplicados
- no union distinct, cada select precisa de where
- intersect - retorna somente o que retorna em ambas tabelas

## Joins
ao inves de fazer join com `a.id = b.id`, podemos usar `USING(id)`

- inner join / join = dado tem que existir nas duas tabelas, relacao entre tabelas é obrigatoria
- left/right join = não precisa ter relacao na tabela contraria, vai trazer todos os dados da posicao do join e se tiver na contraria, vai trazer, mas não é obrigatorio
- full join = vai trazer com relacao e sem relacao tambem

## CTE
- CTE quando executada uma vez, é armazenada na memória, melhorando desempenho das consultas
