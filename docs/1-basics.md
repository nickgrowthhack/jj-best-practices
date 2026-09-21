# Basics

Jujutsu é um sistema de controle de versão usado pelo comando `jj`, compatível com repositórios Git.

Neste estudo, seguimos o [Squash Workflow](https://steveklabnik.github.io/jujutsu-tutorial/real-world-workflows/the-squash-workflow.html), adaptado para **experimentar primeiro, organizar e descrever depois**.

## 1. Experimente

Com o Jujutsu inicializado, comece em uma mudança local vazia e editável. Os arquivos em que você trabalha, a **working copy**, já correspondem a um commit. Ao executar comandos, o `jj` registra as edições localmente.

- `@` é o commit da working copy, onde você experimenta.
- `@-` é seu pai, o commit imediatamente anterior neste fluxo.

Edite e salve os arquivos. Imagine que, mexendo no `README.md`, você acabou corrigindo o título e esclarecendo uma instrução de uso. Agora veja o que fez:

```sh
jj diff
```

O comando mostra as diferenças entre `@` e `@-`. É nesse momento que você reconhece os resultados que vale a pena separar.

## 2. Separe uma descoberta

Crie um destino vazio para o primeiro resultado:

```sh
jj new --before @ --no-edit
```

Esse comando insere um commit vazio imediatamente antes de `@`. Ele passa a ser `@-`. Você continua na mesma working copy, com todas as edições disponíveis.

Escolha o que vai para esse destino:

```sh
jj squash -i
```

Na seleção interativa, expanda o `README.md` para ver seus trechos. Marque apenas a correção do título e confirme. Ela passa para `@-`, enquanto a melhoria da instrução permanece em `@`. O arquivo continua com as duas melhorias.

Agora descreva o resultado separado e confira seu conteúdo:

```sh
jj describe @- -m "Corrige o título do README.md"
jj diff -r @-
```

`describe` dá uma mensagem ao commit indicado. `diff -r @-` mostra o que esse commit mudou em relação ao próprio pai.

## 3. Repita para a próxima descoberta

Revise o que restou e repita o ciclo, selecionando agora a melhoria da instrução:

```sh
jj diff
jj new --before @ --no-edit
jj squash -i
jj describe @- -m "Esclarece o uso no README.md"
jj diff -r @-
```

Cada repetição cria um novo destino para uma descoberta. Separe resultados coerentes. Se um depender de outro, organize primeiro o que serve de base.

Quando você transfere todas as alterações, o Jujutsu cria uma nova working copy vazia sobre o último resultado. “Vazia” significa sem diferenças em relação ao pai. Os arquivos continuam com todas as melhorias.

Confira a sequência:

```sh
jj log
```

O histórico mostra `@` vazio, a melhoria de uso em `@-` e a correção do título logo abaixo. Você já pode continuar experimentando em `@` ou [publicar os resultados](2-bookmarks.md).
