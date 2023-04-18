---
description: Uma opção de resolução
---

# EXERCÍCIOS Procedure - Resolução

```sql
CREATE PROCEDURE sp_CadastraNotas
	(
		@MATRICULA INT,
		@CURSO CHAR(3),
		@MATERIA CHAR(3),
		@PERLETIVO CHAR(4),
		@NOTA FLOAT,
		@FALTA INT,
		@BIMESTRE INT
	)
	AS
BEGIN

		IF @BIMESTRE = 1
		    BEGIN

                UPDATE MATRICULA
                SET N1 = @NOTA,
                    F1 = @FALTA,
                    TOTALPONTOS = @NOTA,
                    TOTALFALTAS = @FALTA,
                    MEDIA = @NOTA
                WHERE MATRICULA = @MATRICULA
                    AND CURSO = @CURSO
                    AND MATERIA = @MATERIA
                    AND PERLETIVO = @PERLETIVO;
		    END

        ELSE 
        
        IF @BIMESTRE = 2
            BEGIN

                UPDATE MATRICULA
                SET N2 = @NOTA,
                    F2 = @FALTA,
                    TOTALPONTOS = @NOTA + N1,
                    TOTALFALTAS = @FALTA + F1,
                    MEDIA = (@NOTA + N1) / 2
                WHERE MATRICULA = @MATRICULA
                    AND CURSO = @CURSO
                    AND MATERIA = @MATERIA
                    AND PERLETIVO = @PERLETIVO;
            END

        ELSE 
        
        IF @BIMESTRE = 3
            BEGIN

                UPDATE MATRICULA
                SET N3 = @NOTA,
                    F3 = @FALTA,
                    TOTALPONTOS = @NOTA + N1 + N2,
                    TOTALFALTAS = @FALTA + F1 + F2,
                    MEDIA = (@NOTA + N1 + N2) / 3
                WHERE MATRICULA = @MATRICULA
                    AND CURSO = @CURSO
                    AND MATERIA = @MATERIA
                    AND PERLETIVO = @PERLETIVO;
            END

        ELSE 
        
        IF @BIMESTRE = 4
            BEGIN

                DECLARE @RESULTADO VARCHAR(50),
                        @FREQUENCIA FLOAT,
                        @MEDIAFINAL FLOAT,
                        @CARGAHORA INT 
                
                SET @CARGAHORA = (
                    SELECT CARGAHORARIA FROM MATERIAS 
                    WHERE       SIGLA = @MATERIA
                            AND CURSO = @CURSO)

                UPDATE MATRICULA
                SET N4 = @NOTA,
                    F4 = @FALTA,
                    TOTALPONTOS = @NOTA + N1 + N2 + N3,
                    TOTALFALTAS = @FALTA + F1 + F2 + F3,
                    MEDIA = (@NOTA + N1 + N2 + N3) / 4,
                    MEDIAFINAL = (@NOTA + N1 + N2 + N3) / 4,
                    PERCFREQ = 100 -( ((@FALTA + F1 + F2 + F3)*@CARGAHORA )/100)

                    --RESULTADO
                    ,RESULTADO = 
                    CASE 
                        WHEN ((@NOTA + N1 + N2 + N3) / 4) >= 7 
                            AND (100 -( ((@FALTA + F1 + F2 + F3)*@CARGAHORA )/100))>=75
                        THEN 'APROVADO'
                        
                        WHEN ((@NOTA + N1 + N2 + N3) / 4) >= 3 
                            AND (100 -( ((@FALTA + F1 + F2 + F3)*@CARGAHORA )/100))>=75 
                        THEN 'EXAME' 
                        
                        ELSE 'REPROVADO'
                    
                    END

                        WHERE MATRICULA = @MATRICULA
                    AND CURSO = @CURSO
                    AND MATERIA = @MATERIA
                    AND PERLETIVO = @PERLETIVO;


            END
        ELSE 
        
        IF @BIMESTRE = 5

            BEGIN

                UPDATE MATRICULA
                SET NOTAEXAME = @NOTA
                --FALTA CALCULAR O RESULTADO PÓS EXAME
                WHERE MATRICULA = @MATRICULA
                    AND CURSO = @CURSO
                    AND MATERIA = @MATERIA
                    AND PERLETIVO = @PERLETIVO;
            END

		SELECT * FROM MATRICULA	WHERE MATRICULA = @MATRICULA
END

```

Exemplo para testar

```sql
EXEC sp_CadastraNotas @MATRICULA = 1,      -- int
                      @CURSO = 'ENG',      -- char(3)
                      @MATERIA = 'BDA',    -- char(3)
                      @PERLETIVO = '2023', -- char(4)
                      @NOTA = 7.0,         -- float
                      @FALTA = 2,
                      @BIMESTRE = 1;      -- int
GO
EXEC sp_CadastraNotas @MATRICULA = 1,      -- int
                      @CURSO = 'ENG',      -- char(3)
                      @MATERIA = 'BDA',    -- char(3)
                      @PERLETIVO = '2023', -- char(4)
                      @NOTA = 7.0,         -- float
                      @FALTA = 2,
                      @BIMESTRE = 2;      -- int
GO
EXEC sp_CadastraNotas @MATRICULA = 1,      -- int
                      @CURSO = 'ENG',      -- char(3)
                      @MATERIA = 'BDA',    -- char(3)
                      @PERLETIVO = '2023', -- char(4)
                      @NOTA = 7.0,         -- float
                      @FALTA = 2,
                      @BIMESTRE = 3;      -- int
GO
EXEC sp_CadastraNotas @MATRICULA = 1,      -- int
                      @CURSO = 'ENG',      -- char(3)
                      @MATERIA = 'BDA',    -- char(3)
                      @PERLETIVO = '2023', -- char(4)
                      @NOTA = 7.0,         -- float
                      @FALTA = 2,
                      @BIMESTRE = 4;      -- int             


```

```
                      @CURSO = 'ENG',      -- char(3)
```

```
                      @MATERIA = 'BDA',    -- char(3)
```

```
                      @PERLETIVO = '2023', -- char(4)
```

```
                      @NOTA = 7.0,         -- float
```

```
                      @FALTA = 2,
```

```
                      @BIMESTRE = 1;      -- int
```

```
GO
```

```
EXEC sp_CadastraNotas @MATRICULA = 1,      -- int
```

```
                      @CURSO = 'ENG',      -- char(3)
```

```
                      @MATERIA = 'BDA',    -- char(3)
```

```
                      @PERLETIVO = '2023', -- char(4)
```

```
                      @NOTA = 7.0,         -- float
```

```
                      @FALTA = 2,
```

```
                      @BIMESTRE = 2;      -- int
```

```
GO
```

```
EXEC sp_CadastraNotas @MATRICULA = 1,      -- int
```

```
                      @CURSO = 'ENG',      -- char(3)
```

```
                      @MATERIA = 'BDA',    -- char(3)
```

```
                      @PERLETIVO = '2023', -- char(4)
```

```
                      @NOTA = 7.0,         -- float
```

```
                      @FALTA = 2,
```

```
                      @BIMESTRE = 3;      -- int
```

```
                      @FALTA = 2,
```

```
                      @BIMESTRE = 4;      -- int  sq
```

