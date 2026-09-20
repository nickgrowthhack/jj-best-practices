# Bookmarks

Um **bookmark** é um nome que aponta para um commit. O Jujutsu pode gerar esse nome automaticamente ao publicar seu trabalho.

Você pode trabalhar localmente sem bookmarks. Eles entram neste fluxo quando você quer compartilhar o trabalho com um remoto.

## 1. Desenvolver localmente

O ciclo continua sendo o do capítulo anterior: editar e salvar, revisar com `jj diff`, descrever o resultado com `jj describe` e começar a próxima mudança com `jj new`.

Você pode repetir esse ciclo e acumular vários commits antes de publicar. Um bookmark no último commit permite compartilhar toda essa sequência.

## 2. Publicar pela primeira vez

No capítulo anterior, você concluiu a correção e executou `jj new`. A correção ficou em `@-`, o pai da mudança atual.

Com um remoto configurado, publique essa correção:

```sh
jj git push --change @-
```

O Jujutsu gera o bookmark e envia o commit e os ancestrais necessários ao remoto. A mudança vazia em `@` continua pronta para receber novas edições.

No remoto Git, o bookmark aparece como uma branch. A integração desse trabalho em `main` é uma etapa separada.

Para conferir o bookmark no histórico:

```sh
jj log
```

## 3. Continuar o mesmo trabalho

Depois dessa publicação, `@` é a mudança vazia e `@-` é o commit com o bookmark. Neste exemplo, há apenas esse bookmark no commit.

Para acrescentar um ajuste ao mesmo trabalho, edite e salve os arquivos. Revise e descreva o resultado:

```sh
jj diff
jj describe -m "Complementa a explicação no README.md"
```

O ajuste está em `@`, mas o bookmark continua no pai. Antes de executar `jj new`, avance o bookmark para incluir esse ajuste:

```sh
jj bookmark move --from @- --to @
```

`--from @-` seleciona os bookmarks do pai e `--to @` indica o novo destino. Assim, você reutiliza o nome que o Jujutsu gerou sem precisar digitá-lo.

Prepare a próxima mudança e publique a atualização:

```sh
jj new
jj git push --revision @-
```

Agora o ajuste e o bookmark estão em `@-`. `--revision @-` publica os bookmarks existentes nesse commit, atualizando a mesma branch no remoto. Use `jj log` para conferir.

Repita essa sequência a cada novo ajuste desse trabalho. A ordem importa: avance o bookmark enquanto o ajuste ainda está em `@`, depois execute `jj new` e publique.

Usar `--change` em uma nova mudança geraria outro bookmark. Por isso, neste fluxo, usamos `--change` na primeira publicação e `--revision` depois de avançar o bookmark existente.
