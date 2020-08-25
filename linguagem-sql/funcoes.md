# FUNÇÕES

* Uma função é uma sequência de comandos que executa alguma tarefa e que tem um nome. A sua principal finalidade é nos ajudar a organizar programas em pedaços que correspondam a como imaginamos uma solução do problema.

Exemplo de um Função Simples:

```text
CREATE FUNCTION fnRetornaAno (@data DATETIME)
RETURNS int
AS
  BEGIN
  DECLARE @ano int
  SET @ano = YEAR(@data)

      RETURN @ano

END
```

* Chamada ou execução da função

```text
SELECT dbo.fnRetornaAno(GETDATE())

SELECT dbo.fnRetornaAno(Clientes.ClienteNascimento) FROM dbo.Clientes
```

Exemplo de um Função com mais de um parâmetro de entrada: