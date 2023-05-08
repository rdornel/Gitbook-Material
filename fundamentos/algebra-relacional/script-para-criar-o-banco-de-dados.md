# Script para criar o banco de dados





```
group: AlgebraRelacional

Conta = {
	Nome_Agencia:string, Numero_Conta:string, saldo:number

	Joinville,C-100, 500
	Blumenau, C-200, 800
	'Beira Mar', C-250, 400
	'Universitária', C-300, 300
	'Criciúma', C-400, 900
	'Verde Vale', C-800, 550
	'Cidade das Flores', C-900, 1000
}

Agencia = {
	Nome_Agencia:string, Cidade_Agencia:string, fundos:number

	'Verde Vale',Blumenau, 900000
	'Cidade das Flores',Joinville, 800000
	'Universitária', 'Florianópolis', 750000
	Joinville, Joinville, 950000
	'Beira Mar', 'Florianópolis', 600000
	'Criciúma', 'Criciúma', 500000
	Blumenau, Blumenau, 1100000
	'Germânia', Blumenau, 400000
}

Cliente = {
	Nome_Cliente:string, Rua_cliente:string, Cidade_cliente:string
	
	'Ana', 'XV de Novembro','Joinville'
    'Laura','07 de Setembro','Blumenau'
    'Vânia','01 de Maio','Blumenau'
    'Franco','Felipe Schmidt','Florianopolis'
    'Eduardo', 'Beria Mar Norte', 'Florianópolis'
    'Bruno', '24 de maio','Criciúma'
    'Rodrigo','06 de agosto','Joinville'
    'Ricardo','João Colin','Joinville'
    'Alexandre','Margem esquerda','Blumenau'
    'Luciana','Estreito','Florianópolis'
    'Juliana','Iririu','Joinville'
}

Depositante = {
	Nome_cliente:string, Numero_Conta:string
	
	'Ana','C-100'
    'Laura','C-200'
    'Eduardo','C-250'
    'Bruno','C-400'
    'Rodrigo','C-900'
    'Vânia','C-800'
    'Luciana','C-300'
}

Emprestimo = {
	Nome_Agencia:string, Numero_emprestimo:string, Total:number
	
	'Joinville','L-10',2000
   'Blumenau','L-20',1500
    'Beira Mar','L-15',1800
    'Criciúma','L-30',2500
    'Cidade das Flores','L-40',3000
    'Verde Vale','L-35',2800
    'Universitária','L-50',2300
}	

Devedor = {
	Nome_cliente:string, Numero_emprestimo:string

	'Ana','L-10'
	'Laura','L-20'
	'Eduardo','L-15'
	'Bruno','L-30'
	'Rodrigo','L-40'
	'Vânia','L-35'
	'Luciana','L-50'
}
```
