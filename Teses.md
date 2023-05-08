Pensar fazer doutoramento

Falar com profs sobre ser monitor

Design by Contract applied to security
- Usar design by contract para controllar o efeito de funcaoes no sistema em geral
- Uma funcao com efeitos especificos poder ser verifcados
	1. Função adicionar dinheiro a uma conta -> Altera um campo na base de dados
	2. Função remover conta -> Remove uma entrada base de dados
	3. Pedido HTML -> Garantir que nao ocorre XSS

Fuzzing with steady state GA
- ja foi feito mas acho que posso melhorar
- Genetic algorythm


# Implementing design by contract to protect against ()

Concepts
- What i want to do
- How i am going to do it

## TODO
Security
- Decide on a specific attack subset

Auto Contracts
- Decide if i want to try to autogenerate contracts
1. How do i generate contracts automatically
2. Using liquid types?
3. How does my idea switch from (a cena do VV)
- Should i do static analysis (probably considering what alcides said about static-dynamic being comparable)

RunTime vs CompilerTime
- Decide on a laguage (prob rust)

