# Basics

Jujutsu é um sistema de controle de versão usado pelo comando `jj`, compatível com repositórios Git. Aqui seguimos o [Edit Workflow](https://steveklabnik.github.io/jujutsu-tutorial/real-world-workflows/the-edit-workflow.html): trabalhar diretamente em uma mudança e começar outra quando necessário.

## 1. Trabalhar na mudança atual

Os arquivos em que você trabalha, a **working copy**, já correspondem a um commit, representado por `@`. Ao executar comandos do `jj`, as edições salvas são registradas nessa mudança local.

Para começar uma tarefa, crie uma mudança com uma descrição:

```sh
jj new -m "Corrige o título do README.md"
```

`new` cria uma mudança sobre a atual e passa a trabalhar nela. Ela começa vazia, sem diferenças em relação ao pai.

Se `@` já estiver vazio e pronto para essa tarefa, basta usar `jj describe -m "Corrige o título do README.md"` para definir sua descrição.

Edite o arquivo, salve e revise o que mudou:

```sh
jj diff
```

Você pode continuar editando e revisando a mesma mudança. Quando estiver satisfeito, ela está pronta em `@`. Use `jj new -m "Descrição da próxima tarefa"` somente quando for começar outra tarefa.

## 2. Retomar uma mudança

Para retomar uma mudança local editável, encontre-a no histórico:

```sh
jj log
```

O **Change ID** identifica a mudança e permanece enquanto você a revisa. Use esse identificador no lugar de `<change-id>`:

```sh
jj edit <change-id>
```

Essa mudança passa a ser `@`, e as próximas edições atualizam seu conteúdo.

Para publicar a mudança concluída, siga para [Bookmarks](2-bookmarks.md).
