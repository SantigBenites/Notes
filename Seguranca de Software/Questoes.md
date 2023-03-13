# Apresentacao 1

# Apresentacao 2

Como e que o atacante sabe of phisical adress do bloco de memoria da vitima, ou usa blocos previamente documentados?

Como e que sabemos que os delays que o COW cria derivao do COW e nao de latencia ao servidor

Como e que os dados enviados ao servidor sao criados de modo a serem encontradas copias no servidor

# Apresentacao 3

Dado que as vulnerabilidades do C continuam a existir, nao deveriam apenas developers dar port das apps para linguagens mais seguras?

Este tipo de vulnerabilidades nao deriva de mas api de transicao entre secure laguages e C?

# Apresentacao 4

Porque razao o Midas faz copias de pages e nao de objeto ja que usar paginas pode levar a false sharing?

how does midas affect performance compared to other mitigations of double fetch vulnerability?    

Can midas defend against muti threaded writes, and how does it prevent diferent threads from writing to the vulnerable adress?

Can midas lead to deadlocks considering it prevents writes in variables?

# Apresentacao 5

Quando dizem sites EU ou USA, querem dizer servidores nesse paises, empresas sediadas nesses paises, ou utilizadores que se encontravam nesses paises?

# Minha Apresentacao

## Part1
ampfuzz -> finds amplificaiotn DDOS proactively
Assume everyone knwos what DDOS is and fuzzer

## Part2
The targets dont crash unlike fuzzer they just give big response and restart
This not good

In sockets too soon bad, socket not open, too late, wasting time
To solve problem, we send package when socket ready, for this a func was created to warn the fuzzer when the can send package

## Part3
All this taks about getting reponses not how big they are.
For this purpose they have 2 good thigs
	Use protocols with big ratios small sent big response
	Try to trim parts unnessary to the sent - This because sometimes bytes are unessacry


after discovering such a vulnerability, what can be 
done to correct it?
- na generalidade 2 opções, limitar velocidade dos 
pacotes e limitar tamanho dos pacotes (acho que 
falta uma?)
why was greybox fuzzing selected instead of other types of fuzzing?
- to avoid being network protocol dependent, a method 
that instrumented the program with a way to know

why weren't the programs altered in way that the fuzzing happens while still letting the program loop be executed as
usual?
- because pre existing fuzzing stacks were used and these expect the programs to be one-shot programs.
If they didnt transform the programs into one shot programs they would have to basicaly write their own fuzzer
ParmeSan (Angora)

what are the limitations of ampfuzz?