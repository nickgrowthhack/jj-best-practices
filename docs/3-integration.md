# Integrar na main

`main` é o bookmark da linha principal do projeto. Integrar o trabalho significa fazer essa linha incluir os commits que você concluiu.

## 1. Ponto de partida

No final do capítulo anterior, o trabalho concluído está em `@-` e `@` é uma mudança vazia. Vamos integrar essa sequência na `main`.

Este exemplo considera o remoto `origin` configurado, a `main` local acompanhando `main@origin` e a publicação direta permitida. O trabalho forma uma sequência linear, sem outras tarefas pendentes.

## 2. Atualizar a base

Busque as atualizações do remoto:

```sh
jj git fetch --remote origin
```

Como a `main` local acompanha `main@origin`, ela recebe os avanços da linha principal. Agora, reaplique sua sequência de trabalho sobre essa base:

```sh
jj rebase --onto main
```

O `rebase` coloca seus commits depois da `main` atualizada. Neste fluxo, o trabalho concluído continua em `@-` e a mudança vazia continua em `@`.

Se algum comando indicar conflitos, interrompa a sequência e entenda a causa antes de continuar.

## 3. Revisar e integrar

Revise o conjunto das alterações que entrará na `main`:

```sh
jj diff --from main --to @-
```

Confira se o resultado corresponde ao trabalho pretendido e execute as verificações do projeto. Continue apenas quando a revisão e as verificações estiverem concluídas.

Avance a `main` até o último commit do trabalho:

```sh
jj bookmark move main --to @-
```

Esse comando integra o trabalho localmente, fazendo a `main` apontar para o commit que inclui toda a sequência. Para publicar essa posição no remoto:

```sh
jj git push --remote origin --bookmark main
```

Se o push for rejeitado, a publicação não foi concluída. Interrompa a sequência e entenda a causa antes de tentar novamente.

## 4. Continuar trabalhando

Após o push bem-sucedido, confira o histórico:

```sh
jj log
```

A `main` deve estar em `@-`, com o trabalho integrado e publicado. A mudança `@` continua vazia, sobre a `main`, pronta para a próxima tarefa. Você pode começar a editar nela, sem executar outro `jj new`.
