# Git Reset

Funcionamento, sintaxe e aplicação do comando git reset;

## Funcionamento

O `git reset` é uma ferramenta versátil para desfazer alterações, manipulando as "três árvores" do Git: Histórico de Commits (HEAD), Índice de Staging e Diretório de Trabalho.

  * **Mecanismo:** Move o ponteiro do branch atual e do HEAD para um commit específico.
  * **Modos de operação:**
      * `--soft`: Move o HEAD. Mantém o Staging e o Diretório de Trabalho intactos (as alterações voltam como "staged", prontas para commit).
      * `--mixed` (Padrão): Move o HEAD e reseta o Staging. Mantém o Diretório de Trabalho (as alterações voltam como "modified", não preparadas).
      * `--hard`: Move o HEAD e reseta tanto o Staging quanto o Diretório de Trabalho. Descarta todas as alterações permanentemente.

## Sintaxe

```bash
# Resetar um arquivo específico do staging
git reset <arquivo>

# Resetar o repositório para um commit específico com modo
git reset [--soft | --mixed | --hard] <commit>
```

## Exemplos Práticos

**1. Retirar arquivo do Staging (Unstage)**
Útil quando você dá `git add .` por engano e quer remover um arquivo da preparação sem perder o código.

```bash
# Adiciona tudo
git add .

# Remove apenas 'segredos.env' do staging, mantendo o arquivo na pasta
git reset segredos.env
```

**2. Desfazer último commit (Soft)**
Útil para corrigir uma mensagem de commit ou adicionar mais arquivos ao commit anterior sem perder o trabalho feito.

```bash
# Desfaz o último commit, mas mantém os arquivos verdes (staged)
git reset --soft HEAD~1

# Agora você pode fazer alterações e commitar novamente
git commit -m "Nova mensagem correta"
```

**3. Agrupar commits locais (Mixed)**
Útil para limpar um histórico de "trabalho em progresso" antes de finalizar a tarefa.

```bash
# Você fez 3 commits pequenos de teste
# Volta 3 commits, arquivos ficam modificados na sua máquina
git reset --mixed HEAD~3

# Adiciona tudo de uma vez para um único commit limpo
git add .
git commit -m "Funcionalidade completa refatorada"
```

**4. Descartar alterações (Hard)**
Útil para jogar fora um experimento que deu errado.

```bash
# Apaga todas as alterações (commitadas ou não) e volta 2 commits
git reset --hard HEAD~2
```

## Aplicação

  * **Correção local:** Alterar commits recentes que ainda não foram compartilhados.
  * **Organização:** "Atomizar" ou agrupar commits para deixar o histórico mais limpo.
  * **Gerenciamento de Staging:** Retirar arquivos adicionados incorretamente à área de preparação.
  * **Limpeza:** Restaurar o projeto para um estado limpo e conhecido.

## Cuidados

  * **Perda de dados (`--hard`):** O modo hard é destrutivo. Qualquer alteração no diretório de trabalho ou staging que não tenha sido salva em outro lugar será perdida para sempre.
  * **Histórico Público:** **Nunca** use `git reset` em commits que já foram enviados (push) para um repositório remoto compartilhado. Isso reescreve o histórico e causará conflitos graves para outros desenvolvedores. Para reverter commits públicos, use `git revert`.

## Referência

  * Atlassian - Git Reset 