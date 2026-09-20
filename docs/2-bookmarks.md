# Bookmarks

Um **bookmark** é um nome que aponta para um commit. O Jujutsu pode gerar esse nome automaticamente ao publicar seu trabalho.

Você pode trabalhar localmente sem bookmarks.

## Publicar o trabalho

No capítulo anterior, você concluiu a correção e executou `jj new`. A correção ficou em `@-`, o pai da mudança atual.

Com um remoto configurado, publique essa correção:

```sh
jj git push --change @-
```

O Jujutsu gera o bookmark e envia o commit e os ancestrais necessários ao remoto.

Para conferir o bookmark no histórico:

```sh
jj log
```
