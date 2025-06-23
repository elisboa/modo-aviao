# Programação em modo-avião
_(um pequeno how-to)_

#### _Disclaimer_

Eu não sou um programador ou desenvolvedor profissional. Esta publicação se destina a quem precisa programar ou manter algum código alheio, mas não tem tanta familiaridade com o assunto

---

## Introdução

Um bom código deve ter algum padrão que facilite o entendimento por quem não esteja tão familiarizado com o objetivo do projeto em questão.

Penso então que seria possível fazer um paralelo com uma viagem de avião. Ou seja, o código pode ser separado em determinadas "fases", onde cada uma teria um objetivo bem definido. Isto ajudaria a entender melhor o que o projeto, classe ou função –– vamos chamar de bloco de código a partir de agora –– deveria fazer, além de separar melhor tudo aquilo que não fosse a essência, o núcleo, o _core_ do código.

A ideia principal é tratar as dependências ou até mesmo códigos "acessórios" em locais diferentes, para facilitar o entendimento ou o _troubleshooting_ –– pra que usar essa palavra tão difícil se temos **diagnóstico**, né? Afinal, se até o próprio autor do código se esquece dele depois, imagina como se sente uma outra pessoa ao tentar entender aquela maçaroca toda?

---

## Os quatro pilares fundamentais

Agora que já falei demais  e tenho certeza que ninguém sobreviveu à introdução e chegou até aqui, vamos falar da essência dessa ideia maluca que é comparar a execução de um código a uma viagem de avião.

O objetivo não é otimizar o código para que ele rode melhor ou mais rápido. É tão somente deixá-lo legível para as futuras gerações ou, melhor ainda, para o seu Eu do futuro, que vai ter que debugá-lo sem tempo e tendo que resolver alguma crise urgente. Em resumo, podemos entender que o foco é mais nas "regras de negócio" do que na otimização técnica do código em si.

Como vamos imitar uma viagem de avião, o que iremos fazer é abstrair o código de maneira que ele passe pelas fases de uma viagem de avião, que no meu limitad{o,íssimo} entender, seriam quatro:

### 1. Verificação pré-vôo (ou pre-flight check, como a gente vê no Terraform, por exemplo)

Esta é a fase em que todas as condições ideais para o vôo são verificadas, todas as variáveis são iniciadas. É importante que NENHUM CÓDIGO SEJA EXECUTADO NESTE MOMENTO, pois como sabemos, o avião está desligado.

Quando eu falo em não executar nenhum código, é num sentido mais abstrato: nenhuma lógica do código ou regra de negócio em si devem ser executados; porém todas as verificações devem ser feitas.

É... isso ficou meio confuso. Vamos dar um exemplo para sermos mais didáticos. Nesta fase, a gente:

- declara variáveis
- faz uma série de `if`/`else` e afins para verificar se o ambiente está disponível para que o código seja executado. Desta maneira, quando ele for executar, não vamos nos preocupar com coisas menores, apenas com o código em si.

**O essencial é que neste momento façamos apenas coisas que não gerem nenhum tipo de alteração no ambiente.**

### 2. Decolar (ou alçar vôo, enfim... o _climbing_)

Neste momento, vamos botar o avião pra subir. Aqui, nós inicializamos o ambiente  a fim de garantir que tudo está certinho e se der qualquer problema, pulamos a próxima fase, indo direto para os procedimentos de aterrissagem.

PS: como não sou programador profissional –– nem conheço tanto a abstração de programação orientada a objeto ––, entenda que todo o meu foco é de alguém com visão de programação orientada a funções, ou algo assim. Sou apenas um _sysadmin_.

Voltando ao assunto... Aqui, nós iremos:
- criar arquivos, diretórios
- testar conexões a serviços externos
- validar permissões de acesso

Vamos, de fato, preparar e garantir a integridade de todo o cenário necessário para que nosso aviãozinho alce voo com toda a segurança possível.

### 3. Voo de cruzeiro

É aqui que a coisa fica interessante: nesta fase da nossa viagem é que vamos, de fato, colocar toda a lógica do código em prática. Uma vez livres de todas as outras preocupações, vamos apenas executar as funções necessárias durante o voo. 

É aqui que servimos o lanchinho ao passageiro, informamos a ele as condições do clima e o tempo estimado de chegada. Vamos concentrar nesta fase tudo que é necessário para, de fato, fazer o que nos propusemos a fazer.

Em resumo, é aqui que o código da aplicação é colocado, de fato.

### 4. Aterrissar –– ou pousar ou qualquer outra palavra que remeta a terminar o pouso

Neste momento, nossa únca preocupação deve ser pousar nosso aviãozinho da melhor maneira possível. Ou seja, iremos realizar aqui todo o tratamento de erros, limparemos todo o lixo que geramos e desfaremos todos os nós e amarrações (conexões a serviços) antes feitos. Sei que linguagens mais modernas já vão ter isso num bloco `try...catch`, mas aqui estamos intencionalmente criando à nossa própria maneira.

É uma fase de faxina e encerramento mesmo, então não vamos ter que nos preocupar com absolutamente nada que não seja terminar a execução do programa –– ou bloco de código.

Aqui nós trataremos os erros, geraremos logs e tudo aquilo que for relativo à finalização do sistema. Nenhuma lógica principal deverá ser aplicada aqui. Apenas procedimentos de término/deleção/encerramentos, mesmo.

Em um código procedural, pode fazer mais sentido que isto seja uma fase própria. Já em linguagens com orientação a objeto, onde podemos ter blocos de "try…catch", pode fazer mais sentido entender que todo procedimento deve ter um controle de fluxo ou uma verificação de erro para que o código saiba tratar a maioria dos erros. Ou seja, pode ser algo parecido com a programação orientada a testes, também.

---

## Explicação (rasa) sobre esta ideia maluca

Como dito antes, este jeito de se organizar o código tem como objetivo apenas facilitar a localização de partes específicas de um projeto, de maneira a facilitar seu entendimento. É claro que isto é extremamente subjetivo e cada um pode achar melhor fazer desse ou daquele jeito. Pode até mesmo achar isso doido demais e até mesmo inaplicável a sua vida.

No momento em que escrevo essas ideias, estou eu mesmo me propondo um desafio. Eu tenho em mente que é possível fazer isso em funções ou projetos mais simples, como conectar-se a um banco de dados e obter informações de lá, ou até mesmo conectar-se a um servidor de arquivos, trazer coisas de lá, processar e então enviá-las para outro lugar, já processadas.

Mas meu objetivo é por à prova essa ideia em um projeto um pouco mais complexo e (também) subjetivo: meu projeto [linux-time-machine](github.com/elisboa/linux-time-machine.sh). Ele já se encontra plenamente funcional, mas foi escrito antes de eu pensar nesta ideia. Então, no momento vou me dedicar a reescrevê-lo aplicando estes conceitos, para depois voltar e atualizar este documento. Ele está sendo reescrito [neste novo repositório](https://github.com/elisboa/tmgit)

---

## Conclusão

Resumo: eu tive uma ideia maluca, resolvi escrever sobre ela para não perdê-la, e agora vou tentar aplicá-la.

Sendo um pouco mais abrangente, eu diria que esta ideia pode ser aplicada tanto a um projeto mais complexo quanto a partes pequenas de um projeto, como algumas funções ─ ou classes ─ específicas, mas devido ao seu alto nível de subjetividade, pode não ser tão fácil.

Como hoje é só uma ideia, estamos na fase de tentar torná-lo funcional para termos de fato um caso de uso que o justifique.

---

## Projetos que utilizam essa metodologia

Hoje existe apenas um projeto de acesso público, de minha autoria, que utiliza esta metodologia. Seu objetivo é validá-la, de fato.

O projeto é o [tmgit](https://github.com/elisboa/tmgit), que pretende ser uma versão reescrita do projeto [linux-time-machine](github.com/elisboa/linux-time-machine.sh).

Além disso, também tenho usado esta metodologia em scripts menores de uso privado em meu trabalho. Neste caso, não crio arquivos separados para cada fase; apenas divido-as em funções dentro do mesmo arquivo.

---
