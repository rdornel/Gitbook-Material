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


```text 
CREATE FUNCTION DtsMinutos(@min int, @dti datetime, @dtf datetime)
RETURNS @tbl TABLE(dt datetime)
AS
BEGIN
    WHILE @dti <= @dtf
    BEGIN
      INSERT INTO @tbl(dt) VALUES (@dti)
      SET @dti = DATEADD(MINUTE,@min,@dti)
    END      
    RETURN
END
```

Exemplo de um Função que retorna uma tabela:

```text
CREATE FUNCTION funcionariosApos(@dt datetime)
RETURNS TABLE
AS
RETURN (SELECT *
        FROM  FUNCIONARIO
        WHERE dataContratacao >= @dt)
```