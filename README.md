# Git Merge
## Funcionamento, sintaxe e aplicação do comando git merge

## 1. Funcionamento e Propósito

O comando **git merge** integra duas linhas de desenvolvimento, combinando os históricos de *branches*. É usado para unir código, consolidar commits e garantir que funcionalidades concluídas sejam integradas com segurança.

### Funções Principais

- **Unificação do código:** integra branches de feature/bugfix às branches principais.
- **Mesclagem de histórico:** combina commits e registra o progresso.
- **Controle de qualidade:** permite evolução entre ambientes (develop → hml → main).
- **Resolução de conflitos:** força decisões manuais quando partes do código foram alteradas por mais de uma pessoa.

---

## 2. Sintaxe e Aplicação

### HEAD no merge
O **HEAD** aponta para o commit atual.  
Durante conflitos, ele representa o “lado atual” do merge:

```
<<<<<<< HEAD
```

### Sintaxe básica

```bash
git merge <branch>
```

### Processo correto

1. Estar na branch de destino:

```bash
git checkout main
```

2. Executar o merge:

```bash
git merge feature-login
```

### Atualizar antes de integrar

```bash
git checkout main
git pull
git merge feature-x
```

### Merge com branch remota

```bash
git merge origin/main
```

### git pull = git fetch + git merge

---

## 3. Tipos de Merge

### Fast-forward
O histórico é linear e o Git apenas move o ponteiro:

```
(main) → (feature)
```

### 3-way merge
Usado quando a branch de destino teve novos commits.  
Cria um **commit de merge** preservando o contexto.

---

## 4. Flags Importantes

### Merge com --no-ff

```bash
git merge --no-ff <branch>
```

Sempre cria um commit de merge.  
Uso comum com Git Flow para rastrear funcionalidades.

### Merge com --squash

```bash
git merge --squash feature-x
git commit -m "Adiciona feature X"
```

Agrupa todos os commits da feature em **um único commit**, útil para manter a história limpa.

---

## 5. Conflitos de Merge

### Como o Git marca conflitos

```
<<<<<<< HEAD
seu código
=======
código da branch mesclada
>>>>>>> feature
```

### Como resolver

1. Editar manualmente.
2. Marcar como resolvido:

```bash
git add <arquivo>
```

3. Finalizar o merge:

```bash
git merge --continue
```

### Abortar o merge

```bash
git merge --abort
```
### Fonte  
Documentação oficial do Git sobre o comando **git merge**: https://git-scm.com/docs/git-merge  