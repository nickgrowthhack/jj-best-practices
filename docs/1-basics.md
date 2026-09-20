# Basics

## 1. O que é o Jujutsu

Jujutsu é um sistema de controle de versão usado pelo comando `jj`. Ele pode trabalhar com repositórios Git e compartilhar commits com pessoas que continuam usando Git, inclusive pelo GitHub.

A principal funcionalidade está na forma de organizar o trabalho local. Você pode construir uma mudança aos poucos, revisar seu conteúdo e decidir quando começar a próxima.

## 2. O que muda no jeito de trabalhar

No Jujutsu, os arquivos em que você trabalha, a **working copy**, já correspondem a um commit. Conforme você edita, esse commit é atualizado.

A maioria dos comandos `jj` registra as alterações salvas nos arquivos antes de executar sua ação. Isso acontece, por exemplo, quando você roda `jj status`. O Jujutsu não salva o conteúdo que ainda está apenas no editor.

Não há etapa de staging nesse fluxo. Você não precisa executar o equivalente a `git add` para preparar cada alteração. Por padrão, arquivos novos também entram automaticamente, respeitando o `.gitignore`.

O registro é local. Rodar esses comandos não publica seu trabalho no GitHub.

## 3. Como se localizar

Uma **change** é uma mudança que pode evoluir mantendo sua identidade. Ela tem dois identificadores:

- **Change ID:** permanece enquanto você revisa a mesma mudança.
- **Commit ID:** é o hash conhecido do Git. Muda quando o conteúdo ou a mensagem do commit muda.

Ao consultar o histórico, prefira reconhecer a mudança pelo change ID. O hash identifica uma versão específica dela.

Dois símbolos ajudam a localizar seu trabalho:

- `@` representa o commit da working copy, onde você está trabalhando.
- `@-` representa seu pai, no fluxo simples com um único pai.

Use estes comandos para se orientar:

| Comando | O que mostra |
| --- | --- |
| `jj status` | Os arquivos alterados, o commit atual e seu pai. |
| `jj diff` | As diferenças de conteúdo entre o commit atual e seu pai. |
| `jj log` | Um grafo do histórico, com `@` indicando sua posição. |

## 4. Um ciclo básico

Imagine uma tarefa pequena: corrigir o título do `README.md`. Comece com uma mudança atual vazia, edite o arquivo e salve. Depois, revise:

```sh
jj status
jj diff
```

Confira se a alteração corresponde à tarefa. Se precisar ajustar algo, edite, salve e revise novamente. As alterações continuam pertencendo à mesma mudança.

Quando estiver satisfeito, descreva o resultado:

```sh
jj describe -m "Corrige o título do README.md"
```

`describe` define a mensagem do commit atual. Você pode continuar editando essa mudança depois de descrevê-la.

Para começar a próxima tarefa, execute:

```sh
jj new
```

`new` cria uma mudança vazia sobre a atual e passa a trabalhar nela. A correção do `README.md` fica no pai, `@-`. As próximas edições entram no novo `@`.

Os arquivos continuam com o título corrigido. “Vazia” significa que a nova mudança ainda não tem diferenças em relação ao pai. Use `jj log` para conferir essa sequência.

## 5. O próximo passo

Um **bookmark** é um nome que aponta para um commit, como uma branch no Git. Ao compartilhar trabalho com um repositório Git, bookmarks correspondem às branches.

Você pode criar mudanças locais sem nomear cada uma com um bookmark. Também não existe um bookmark ativo que avance automaticamente a cada `jj new`, como uma branch ativa no Git.

O próximo passo é publicar seu trabalho usando um bookmark gerado automaticamente.
