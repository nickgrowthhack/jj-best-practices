# Bookmarks

Um **bookmark** é um nome que aponta para um commit e corresponde a uma branch no remoto Git.

Você pode trabalhar localmente sem bookmarks. Neste fluxo, o Jujutsu gera o nome automaticamente ao publicar seu trabalho.

## 1. Publicar a mudança atual

Com o repositório inicializado para Jujutsu e um remoto configurado, publique a mudança concluída em `@`, antes de começar a próxima tarefa:

```sh
jj git push --change @
```

O comando gera o bookmark e envia o commit e os ancestrais necessários ao remoto. Publicar outra mudança com `--change` gera outro bookmark.

Para conferir o bookmark no histórico:

```sh
jj log
```
