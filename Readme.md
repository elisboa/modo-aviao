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

A essência da ideia é comparar a execução de um código a uma viagem de avião.

O objetivo não é otimizar o código para que ele rode melhor ou mais rápido. É tão somente deixá-lo legível para as futuras gerações ou, melhor ainda, para o seu Eu do futuro, que vai ter que debugá-lo sem tempo e tendo que resolver alguma crise urgente. Em resumo, podemos entender que o foco é mais nas "regras de negócio" do que na otimização técnica do código em si.

Como vamos imitar uma viagem de avião, o que iremos fazer é abstrair o código de maneira que ele passe pelas fases de uma viagem de avião, que no meu limitad{o,íssimo} entender, seriam quatro:

### 1. Verificação pré-voo (ou pre-flight check, como a gente vê no Terraform, por exemplo)

Esta é a fase em que todas as condições ideais para o voo são verificadas e todas as variáveis são declaradas. O princípio central é: **nenhuma operação que gere alteração no ambiente deve ocorrer aqui**. Nenhuma lógica de negócio, nenhum efeito colateral — apenas leituras e verificações.

Nesta fase, a gente:

- declara variáveis
- faz uma série de `if`/`else` e afins para verificar se o ambiente está disponível para que o código seja executado. Desta maneira, quando ele for executar, não vamos nos preocupar com coisas menores, apenas com o código em si.

### 2. Decolagem (ou alçar voo, enfim... o _climbing_)

Neste momento, vamos botar o avião pra subir. Aqui, nós inicializamos o ambiente a fim de garantir que tudo está em ordem e, se der qualquer problema, pulamos a próxima fase, indo direto para os procedimentos de aterrissagem.

Aqui, nós iremos:
- criar arquivos, diretórios
- testar conexões a serviços externos
- validar permissões de acesso

Vamos, de fato, preparar e garantir a integridade de todo o cenário necessário para que nosso aviãozinho alce voo com toda a segurança possível.

### 3. Voo de cruzeiro

Nesta fase é que colocamos, de fato, toda a lógica do código em prática. Uma vez livres de todas as outras preocupações, vamos apenas executar as funções necessárias durante o voo.

É aqui que servimos o lanchinho ao passageiro, informamos a ele as condições do clima e o tempo estimado de chegada. Vamos concentrar nesta fase tudo que é necessário para, de fato, fazer o que nos propusemos a fazer.

Em resumo, é aqui que o código da aplicação é colocado, de fato.

### 4. Aterrissagem –– ou pouso, ou qualquer outra palavra que remeta a terminar o voo

Neste momento, nossa única preocupação deve ser pousar nosso aviãozinho da melhor maneira possível. Ou seja, iremos realizar aqui todo o tratamento de erros, limparemos todo o lixo que geramos e desfaremos todos os nós e amarrações (conexões a serviços) antes feitos. Sei que linguagens mais modernas já vão ter isso num bloco `try...catch`, mas aqui estamos intencionalmente criando à nossa própria maneira.

É uma fase de faxina e encerramento mesmo, então não vamos ter que nos preocupar com absolutamente nada que não seja terminar a execução do programa –– ou bloco de código.

Aqui nós trataremos os erros, geraremos logs e tudo aquilo que for relativo à finalização do sistema. Nenhuma lógica principal deverá ser aplicada aqui. Apenas procedimentos de término/deleção/encerramentos, mesmo.

> **Nota:** Em scripts lineares ou código procedural simples, faz sentido ter a aterrissagem como uma fase própria e centralizada. Já em código mais modular — funções, classes, métodos —, pode fazer mais sentido que cada unidade trate seus próprios erros com blocos `try...catch`, seguindo uma abordagem de programação defensiva. Neste caso, a fase de aterrissagem ainda existe conceitualmente, mas distribuída ao longo do código.

---

## Formas de organização do código

Atualmente, as seguintes organizações de código foram utilizadas:

1. Dentro do mesmo arquivo
    Nesta forma de organização, em scripts simples, novos ou já existentes, o código foi reorganizado de maneira a representar as fases do voo do avião. Na maioria dos casos, as fases de decolagem e voo de cruzeiro (2 e 3) foram mescladas em uma só, devido à simplicidade ou mesmo o pouco tamanho do código.

2. Arquivos-chave
    Nesta outra forma, foram criados 4 arquivos representando cada fase. Dentro deles, foram criadas as funções relacionadas a cada fase, na ordem em que se tornaram necessárias.
    Exemplos:
    - [tmgit - Time Machine via Git](https://github.com/elisboa/tmgit)
    - [tmgit-py - Time Machine via Git (Python)](https://github.com/elisboa/tmgit-py)

---

## Projetos que utilizam essa metodologia

Atualmente, existem dois projetos de acesso público, de minha autoria, que utilizam esta metodologia:

- [tmgit](https://github.com/elisboa/tmgit) — reescrita do [linux-time-machine](github.com/elisboa/linux-time-machine.sh) em shell, o primeiro caso de uso real desta metodologia.
- [tmgit-py](https://github.com/elisboa/tmgit-py) — reescrita do mesmo projeto em Python, com uma particularidade no processo de desenvolvimento: o Claude AI atua como gerente de projeto, gerando os prompts que guiam o GitHub Copilot na escrita do código. O próprio Claude AI também revisa o código gerado e propõe correções, funcionando como uma camada de controle de qualidade sobre o trabalho do Copilot.

Além disso, também tenho usado esta metodologia em scripts menores de uso privado em meu trabalho. Neste caso, não crio arquivos separados para cada fase; apenas divido-as em funções dentro do mesmo arquivo.

---

## Conclusão

A metodologia é escalável: funciona tanto em scripts simples quanto em projetos maiores, e pode ser aplicada a um projeto inteiro ou apenas a funções e classes específicas. Como qualquer convenção de organização de código, sua adoção depende do contexto — o que importa é que o código seja legível para quem vier depois.

---
