# CURSORES

 Exemplo de um Cursor:

```text
DECLARE @ClienteNome VARCHAR(50), @ClienteSexo CHAR(1), @contador INT=0;

    DECLARE [cursorListaCliente] CURSOR FOR
    SELECT Clientes.ClienteNome , ClienteSexo
    FROM Clientes

    OPEN [cursorListaCliente]
    FETCH NEXT FROM [cursorListaCliente] INTO @ClienteNome, @ClienteSexo;

    WHILE @@FETCH_STATUS = 0
    BEGIN
         SET @contador=@contador+1;

    SELECT @ClienteNome as Nome, @ClienteSexo AS Sexo, @contador;
    FETCH NEXT FROM [cursorListaCliente] INTO @ClienteNome, @ClienteSexo
    END
    CLOSE [cursorListaCliente];
      DEALLOCATE [cursorListaCliente];
```

