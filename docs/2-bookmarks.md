# Bookmarks

Um **bookmark** é um nome que aponta para um commit. O Jujutsu pode gerar esse nome automaticamente ao publicar seu trabalho.

Você pode trabalhar localmente sem bookmarks. Eles entram neste fluxo quando você quer compartilhar o trabalho com um remoto.

## 1. Desenvolver localmente

O ciclo continua sendo o do capítulo anterior: editar e salvar, revisar com `jj diff`, descrever o resultado com `jj describe` e começar a próxima mudança com `jj new`.

Você pode repetir esse ciclo e acumular vários commits antes de publicar. Um bookmark no último commit permite compartilhar toda essa sequência.

## 2. Publicar o trabalho

No capítulo anterior, você concluiu a correção e executou `jj new`. A correção ficou em `@-`, o pai da mudança atual.

Com o repositório inicializado para Jujutsu e um remoto configurado, publique essa correção:

```sh
jj git push --change @-
```

O Jujutsu gera o bookmark e envia o commit e os ancestrais necessários ao remoto. A mudança vazia em `@` continua pronta para receber novas edições.

No remoto Git, o bookmark aparece como uma branch. Publicar outra mudança com `--change` gera outro bookmark.

Para conferir o bookmark no histórico:

```sh
jj log
```
