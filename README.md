# Git Merge
## Funcionamento, sintaxe e aplicação do comando git merge;

## Funcionamento
- O `git merge` integra duas linhas de desenvolvimento, unindo o histórico de branches diferentes.
- O processo compara o histórico da branch atual (HEAD), o histórico da branch a ser mesclada e o *ancestral comum* entre elas.
- O Git analisa diferenças e tenta unir automaticamente o conteúdo.
- Quando há alterações conflitantes, exige resolução manual.
- O resultado pode ser:
  - **Fast-forward:** apenas move o ponteiro da branch.
  - **3-way merge:** cria um *commit de merge* para registrar a união.

## Sintaxe

```bash
git checkout <branch-destino>
git merge <branch-origem>
```

### Exemplo simples

```bash
git checkout main
git merge feature-login
```

### Merge com branch remota

```bash
git merge origin/main
```

### Merge com --no-ff  
Garante um commit de merge mesmo quando seria possível fast-forward.

```bash
git merge --no-ff <branch>
```

### Merge com --squash  
Agrupa todos os commits da branch em apenas um.

```bash
git merge --squash feature-x
git commit -m "Adiciona feature X"
```

## Aplicação

- Integrar código finalizado e revisado às branches principais.
- Unir branches de desenvolvimento, testes ou funcionalidades.
- Controlar a evolução entre ambientes (ex.: develop → hml → main).
- Registrar o ponto exato em que uma feature foi integrada.
- Manter rastreabilidade do desenvolvimento em equipes que usam Git Flow.

3. Finalizar o merge:

```bash
git merge --continue
```

### Abortar o merge

```bash
git merge --abort
```

## Referência

[Git - Merge](https://git-scm.com/docs/git-merge)
