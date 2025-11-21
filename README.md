# Git Checkout
## Funcionamento, sintaxe e aplicação do comando git checkout
## Funcionalidade:

O comando serve para alternar entre os ramos (branches) ou restaurar arquivos da árvore de trabalho. Sua função principal é atualizar os arquivos na árvore de trabalho para que correspondam à versão no índice ou em uma árvore determinada (commit), atualizando também o HEAD para definir o ramo especificado como o atual. Além disso, pode ser usado para criar novos ramos e alternar para eles imediatamente ou para inspecionar commits antigos


## Sintaxe:
```bash
# Mudança entre ramos
git checkout [-q] [-f] [-m] [<ramo>]

# Criar novo ramo
git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <novo-ramo>] [<ponto-de-partida>]

# Modo desanexado (detached HEAD)
git checkout [-q] [-f] [-m] --detach [<ramo>]
git checkout [-q] [-f] [-m] [--detach] <commit>

# Restauração de arquivos
git checkout [-f|--ours|--theirs|-m|--conflict=<estilo>] [<árvore>] [--] <pathspec>…​

# Modo interativo
git checkout (-p|--patch) [<árvore>] [--] [<pathspec>…​]
```

## Aplicação:

#### 1. Troca entre Ramificações
```bash
git checkout develop          # Muda para ramo 'develop'
git checkout -b nova-feature  # Cria e muda para novo ramo
```

#### 2. Restauração de Arquivos
```bash
git checkout arquivo.txt           # Restaura do índice
git checkout HEAD~1 arquivo.txt    # Restaura de commit anterior
git checkout -- '*.js'             # Restaura múltiplos arquivos
```

#### 3. Inspeção de Commits Antigos

```bash
git checkout a1b2c3d              # HEAD desanexado para commit específico
git checkout v2.0                 # HEAD desanexado para tag
```

#### 4. Resolução de Conflitos
```bash
git checkout --ours arquivo.conflict   # Usa nossa versão
git checkout --theirs arquivo.conflict # Usa versão deles
```

#### 5. Modo Interativo para Descarte Seletivo
```bash
git checkout -p  # Descarte interativo de mudanças
```
## Cuidados

Não use `git checkout -f` sem verificar as alterações locais, pois descarta modificações não salvas permanentemente.
No modo "detached HEAD", commits feitos ficam soltos e podem ser perdidos pela coleta de lixo do Git se não forem referenciados.
Ao trocar de branch com conflitos não resolvidos, o checkout pode falhar; use `-m` para tentar mesclagem automática ou resolva os conflitos manualmente primeiro.

## Referência
Git - Checkout