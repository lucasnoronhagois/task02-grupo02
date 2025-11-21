# Git Reset

Funcionamento, sintaxe e aplicação do comando git reset.

## Funcionamento

O `git reset` move o ponteiro HEAD atual para um estado específico e opcionalmente altera o Índice e o Diretório de Trabalho.

**Passos do processo:**

1.  Move o ponteiro HEAD para o commit especificado.
2.  Atualiza o Índice (*Staging Area*) para corresponder ao commit (se não for `--soft`).
3.  Atualiza o Diretório de Trabalho para corresponder ao commit (apenas se for `--hard`).

**Resultado:** Permite desfazer commits, remover arquivos do stage ou limpar o diretório de trabalho.

## Sintaxe

```bash
git reset [<modo>] [<commit>]
```

### Exemplo simples (Padrão/Mixed)

```bash
git reset HEAD^
```

**Significado:** Desfaz o último commit, mas mantém as alterações nos arquivos como "não preparadas" (*unstaged*).

### Exemplo avançado com --hard

```bash
git reset --hard HEAD~3
```

**Significado:** Move o HEAD 3 commits para trás e apaga todas as alterações nos arquivos e no índice. **Destrutivo**.

## Modos principais

  * **`--soft`**: Apenas move o HEAD. Alterações ficam em "staged" (prontas para commit).
  * **`--mixed`** (padrão): Move HEAD e atualiza o índice. Alterações ficam em "modified" (no disco, mas fora do stage).
  * **`--hard`**: Move HEAD, atualiza índice e apaga arquivos. O estado volta exatamente ao do commit alvo.

## Aplicação

  * Corrigir o último commit (`soft`) para adicionar algo esquecido.
  * Desfazer commits locais antes de enviar ao remoto.
  * Remover arquivos do stage (`git add`) sem perdê-los (`mixed`).
  * Descartar experimentos que deram errado (`hard`).

## Cuidados

  * O uso de `--hard` apaga permanentemente trabalhos não commitados.
  * Não use `git reset` em commits já compartilhados (*push*) se outras pessoas dependem deles, pois reescreve o histórico.

## REFERÊNCIA

- [GIT RESET - GIT](https://git-scm.com/docs/git-reset)