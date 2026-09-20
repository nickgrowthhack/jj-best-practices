# Bookmarks

## 1. Para que serve um bookmark

Um **bookmark** é um nome que aponta para um commit. Ele ajuda a identificar um ponto do trabalho sem precisar lembrar seu change ID ou hash.

Criar um bookmark apenas dá um nome a esse ponto. Não cria outra mudança nem altera os arquivos. Você também pode continuar trabalhando em commits que não tenham bookmark.

Neste capítulo, vamos continuar a correção do `README.md` do capítulo anterior, dando um nome ao trabalho e depois avançando esse nome para incluir outro ajuste.

## 2. Criar um bookmark

Ao terminar o capítulo anterior com `jj new`, você ficou nesta situação:

- `@` é uma mudança vazia, pronta para receber novas edições.
- `@-` é o commit com a correção do título do `README.md`.

Vamos chamar esse trabalho de `nick/readme-fix`. Considerando que esse nome ainda não existe, execute:

```sh
jj bookmark create nick/readme-fix -r @-
```

`create` cria o bookmark. A opção `-r` indica o commit de destino, neste caso, o pai da working copy.

Sem `-r @-`, o destino padrão seria `@`. Aqui, queremos nomear a correção concluída, que está no pai. Sua posição de trabalho continua sendo a nova mudança vazia.

## 3. Conferir onde ele está

Consulte os bookmarks e o histórico:

```sh
jj bookmark list
jj log
```

`list` mostra os nomes e os commits para os quais apontam. No grafo de `log`, procure `nick/readme-fix` junto ao commit da correção do título.

Observe também o símbolo `@`. Ele indica onde suas próximas edições entram. O bookmark indica o commit que você escolheu nomear. Essas duas posições podem ser diferentes, como são agora.

Não é necessário mover o bookmark para começar a editar. Você já está na mudança preparada pelo `jj new`.

## 4. Avançar o bookmark

Agora, acrescente ao `README.md` uma frase explicando o objetivo do projeto. Salve o arquivo e revise:

```sh
jj diff
```

O diff deve mostrar apenas o novo ajuste. A correção do título já está no pai e faz parte do ponto de partida.

Descreva esse segundo resultado e prepare a próxima mudança:

```sh
jj describe -m "Explica o objetivo do projeto no README.md"
jj new
```

O segundo ajuste agora está em `@-`. O bookmark continua no primeiro commit, pois criar uma nova mudança não o faz avançar automaticamente.

Para que o nome passe a apontar para o segundo ajuste, execute:

```sh
jj bookmark move nick/readme-fix --to @-
```

`move` atualiza um bookmark existente. `--to` indica o novo destino. Neste exemplo, avançamos para um descendente do commit anterior.

O esquema abaixo mostra o efeito, com os commits mais recentes no topo:

```text
Antes de mover:
@  Próxima mudança, vazia
|
o  Explicação do objetivo
|
o  Correção do título  <- nick/readme-fix

Depois de mover:
@  Próxima mudança, vazia
|
o  Explicação do objetivo  <- nick/readme-fix
|
o  Correção do título
```

Mover o bookmark não troca a working copy nem junta os dois commits. O segundo commit tem o primeiro como ancestral, e ambos continuam no histórico.

Execute novamente `jj bookmark list` e `jj log` para conferir o destino. O símbolo `@` deve permanecer na mudança vazia.

## 5. O que lembrar

- **Criar:** associa um novo nome a um commit.
- **Consultar:** permite conferir a posição desse nome no histórico.
- **Mover:** atualiza o destino de um nome existente.

Bookmarks não avançam automaticamente quando novos commits são criados. Porém, se o commit apontado for reescrito, por exemplo, ao editar sua mensagem, o bookmark acompanha a nova versão daquela mesma mudança.

Até aqui, tudo foi feito localmente. O próximo passo é usar esse bookmark para publicar o trabalho.
