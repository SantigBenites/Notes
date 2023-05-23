# Results

O artigo de depois comeca a avaliacao exprimental
Iniciam por procurar um conjunto de websites vulneraveis
Principalmente procuram websites que utilizassem 2FA e browser fingerprinting, e que usem browser fingerprinting para dar login do user sem usar 2FA
Depois os autores verificaram se os websites escolhidos estavam suscetiveis a este tipo de ataque
Efetivamente este verificaram que dos 300 websites escolhidos apenas 14 usavam browser
fingerprints para autenticar o user, o resto recorriam a cookies
Podemos ver os resultados na tabela seguinte:

## Tabela
2 maiores resultados foram obtidos desta analise

- Cada website usa diferentes metodos para fazer o fingerprinting:
1. Fingerprinting basico, usa informacao sobre o browser e o user
2. Fingerprints mais avancadas, usando a dimensao do canvas, texto, render e settings de audio
Tendo isto em consideracao este metodo e capaz de evitar 2FA em 9 dos 14 sites, e os ultimos 5 so eram capazes de notar a intrusao devido á utilizacao de IP como parte do fingerprinting. (verificam se o IP currente e igual a um dos usados previamente).
Mesmo nestas situacoes podemos dar bypass a esta situacao alterando o header da mensagem para parecer que foi enviado do host original. Este mesmo efeito pode ser obtido usando meios alternativos de alteracao de headers.
Os autores infelizamente nao indicam como este tipo de ataque poderia interagir com proxies.


- Os websites que foram encotrados a usar este tipo de fingerprinting
Todos os websites indentificados estavam todos relacionados com bancos, impostos, online marketing e outros servicos criticos. Criticos na metrica que caso um atacante conseguisse circumventar a autenticacao deste os danos que poderiam ser feitos eram altos, dado que a informacao que este possuem e de alto valor.

# Limitations

Finalmente estes referem nao so as limitacoes mas pontos de contestacao que ocorreram ao longo do research.
Nos retiramos alguns destes que achamos mais relevantes

## Relevance of phishing

Em primeiro lugar, os autores denotam nao so que a quantidade de sites de phising nos dias de hoje esta a aumentar exponencialmente e com metodos cada vez mais avancados, eles afirmam que uma boa quantidade destes recorre a este metodo para falsificar 2FA.

## Fingerprinting extension restrictions

Em segundo lugar, os autores afirmam que o metodo deles para obter fingerprints dos websites esta dependente da utlizacao de biblitoecas populares, e deste modo se o website estiveram a usar uma implemtacao propriertaria era possivel que a extensao nao funcione corretamente

## Possible Denfenses

Em terceiro lugar, apresentacao possiveis defesas tanto para clients como para empresas.
Para clientes nos detacamos a utlizacao sempre de 2FA tendo em consideracao para requesitar 2FA chalange sempre
Para empresas a utilizacao de opt-out em vez de opt-in e capaz de ser a melhor recomendacao, ou seja, usar 2FA em todos os utilizadores e apenas retirar esta autenticacao caso seja pedido.


# Future Work

Os autores referenciam 2 topicos de future work relavantes:

## Chaining sessions

O uso de chaining sessions, ou seja, sessions consequentes nas quais valores como canvas size sao alteradas entre sessions, isto efetivamente nulifica grande parte do risco deste tipo de ataques, embora apresente outros problemas de seguranca

## Trusted Execution Environment

Dada a natureza de browser fingerprints estar relationada com client side, a unica maneira de evitar este tipo de ataques teria de aranjar alguma maneira de evitar possivel spoofing por parte de um atacante. Os autores referem a utilizacao de Trusted Execution Environment como uma possivel idea para uma maneira de evitar este tipo de vulnerabilidade.