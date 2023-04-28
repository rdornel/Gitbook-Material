---
description: Common Table Expression
---

# CTE

Especifica um conjunto de resultados nomeado temporário, conhecido como uma CTE (expressão de tabela comum). Ela é derivada de uma consulta simples e definida no escopo de execução de uma única instrução SELECT, INSERT, UPDATE, DELETE ou MERGE.

Selecioando dados com CTE

```sql
WITH cte_clientes
as
(
SELECT ClienteCodigo 
FROM Clientes
),
cte_cartao
as
(
SELECT ClienteCodigo 
FROM CartaoCredito
)

select cte_cartao.ClienteCodigo, cte_clientes.ClienteCodigo 
from cte_clientes inner join cte_cartao
on cte_cartao.ClienteCodigo=cte_clientes.ClienteCodigo
```

Atualiznado dados usadno CTE

```sql
WITH cte_clientes
as
(
SELECT ClienteCodigo 
FROM Clientes
),
cte_cartao
as
(
SELECT ClienteCodigo 
FROM CartaoCredito
)

UPDATE cte_clientes set ClienteCodigo = cte_clientes.ClienteCodigo 
from cte_clientes inner join cte_cartao
on cte_cartao.ClienteCodigo=cte_clientes.ClienteCodigo
```
