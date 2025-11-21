# Git Revert

Funcionamento, sintaxe e aplicação do comando git revert.

## Funcionamento

O `git revert` cria um **novo commit** que inverte as alterações introduzidas por um commit anterior. Ao contrário do `reset`, ele não apaga o histórico, apenas adiciona uma "correção" no topo.

**Passos do processo:**

1.  Identifica as alterações feitas no commit alvo.
2.  Calcula o inverso dessas alterações (o "anti-diff").
3.  Aplica essas alterações inversas na árvore de trabalho e no índice.
4.  Gera automaticamente um novo commit registrando essa reversão (exceto se usado `-n`).

**Resultado:** O histórico permanece seguro e linear, ideal para desfazer erros em branches compartilhadas.

## Sintaxe

```bash
git revert [<opções>] <commit>
```

### Exemplo simples

```bash
git revert HEAD~3
```

**Significado:** Cria um novo commit que desfaz exatamente o que foi feito no 4º commit anterior (contando a partir do HEAD).

### Exemplo sem commit automático

```bash
git revert -n master~5..master~2
```

**Significado:** Reverte uma sequência de commits, mas **não cria** os novos commits automaticamente. As alterações inversas ficam no seu *stage* (índice) para você revisar e fazer um único commit manual.

## Opções principais

  * **`-e` / `--edit`** (padrão): Permite editar a mensagem do novo commit de reversão.
  * **`--no-edit`**: Não abre o editor de texto; usa a mensagem padrão gerada pelo Git.
  * **`-n` / `--no-commit`**: Aplica a reversão na árvore de trabalho e índice, mas não finaliza o commit. Útil para agrupar várias reversões.
  * **`-m` / `--mainline`**: Obrigatório ao reverter *Merge Commits*. Define qual "lado" da fusão deve ser considerado a linha principal a ser mantida.

## Aplicação

  * Desfazer alterações em branches públicas (ex: `main` ou `develop`) sem quebrar o histórico dos colegas.
  * Remover um bug introduzido em um commit específico antigo, mantendo o trabalho feito depois dele.
  * Documentar explicitamente que uma funcionalidade foi removida/revertida.

## Cuidados

  * **Conflitos:** Se commits posteriores alteraram as mesmas linhas que você está tentando reverter, haverá conflitos para resolver.
  * **Reverter Merges:** Reverter um merge (`-m`) é complexo. Se você reverter um merge, o Git "esquece" as alterações daquele branch. Tentar trazer aquele branch de volta depois é difícil.
  * **Árvore Limpa:** Requer que seu diretório de trabalho esteja limpo (sem arquivos modificados não commitados) antes de rodar.