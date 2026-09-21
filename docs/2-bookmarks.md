# Bookmarks

Um **bookmark** é um nome que aponta para um commit. No remoto Git, ele aparece como uma branch. Neste fluxo, o Jujutsu gera esse nome quando você publica.

No [capítulo anterior](1-basics.md), você separou e descreveu duas descobertas. O último resultado está em `@-`, com o anterior logo abaixo dele. A working copy `@` está pronta para novas experiências.

Com um remoto configurado, publique os resultados:

```sh
jj git push --change @-
```

O comando gera um bookmark para `@-` e envia esse commit e os ancestrais necessários. No exemplo, isso publica as duas melhorias. Qualquer alteração que ainda esteja em `@` permanece local.

Confira o bookmark no histórico:

```sh
jj log
```

Você pode organizar várias descobertas antes de publicar. Usar `--change` para outra mudança gera outro bookmark.
