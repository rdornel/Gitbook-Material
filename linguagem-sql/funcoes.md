# FUNÇÕES

* Uma função é uma sequência de comandos que executa alguma tarefa e que tem um nome. A sua principal finalidade é nos ajudar a organizar programas em pedaços que correspondam a como imaginamos uma solução do problema.

Exemplo de um Função Simples:

```sql
CREATE FUNCTION fnRetornaAno (@data DATETIME)
RETURNS int
AS
  BEGIN
  DECLARE @ano int
  SET @ano = YEAR(@data)

      RETURN @ano

END
```

* Chamada ou execução da função (não esqueça de usar o dbo. antes do nome da função)

```sql
SELECT dbo.fnRetornaAno(GETDATE())

SELECT dbo.fnRetornaAno(Clientes.ClienteNascimento) FROM dbo.Clientes
```

Exemplo de um Função com mais de um parâmetro de entrada:

```sql
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

Exemplo de execução da função

```sql
select * from DtsMinutos(1,getdate(),getdate()+1)

```

Exemplo de um Função que retorna uma tabela:



```sql
CREATE FUNCTION funcionariosApos(@dt datetime)
RETURNS TABLE
AS
RETURN (SELECT *
        FROM  FUNCIONARIO
        WHERE dataContratacao >= @dt)
```

Exemplo de execução

```sql
select * from nascidosApos('1980-01-01') as fn INNER join 
        Clientes on clientes.ClienteNascimento=fn.ClienteNascimento

```

Outros tipos de funções

[https://www.w3schools.com/sql/sql\_ref\_sqlserver.asp](https://www.w3schools.com/sql/sql\_ref\_sqlserver.asp)
