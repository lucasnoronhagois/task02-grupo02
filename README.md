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
# Git Fetch & Git Pull

## Funcionamento, sintaxe e aplicação dos comandos git fetch e git pull;

### Funcionamento
Ambos os comandos são usados para baixar alterações de um repositório remoto (origin) para o seu repositório local. A principal diferença é como eles integram essas mudanças ao seu branch de trabalho.

### Git Fetch
Propósito: Buscar dados do projeto remoto e armazená-los localmente sem alterar o seu branch de trabalho.

Passos do processo:

Conecta-se ao repositório remoto (ex: origin).

Baixa todos os dados do branch remoto (commits, branches, tags) que não estão presentes no seu repositório local.

Armazena esses dados em referências remotas (ex: origin/main).

Resultado: Você pode inspecionar as mudanças remotas (origin/main) antes de aplicá-las ao seu branch local (main).

### Git Pull
Propósito: Buscar dados do remoto e integrá-los imediatamente ao seu branch de trabalho local.

Passos do processo:

Executa o git fetch (baixa os dados do remoto para as referências remotas locais).

Executa uma operação de git merge ou git rebase (integra os dados do branch remoto, ex: origin/main, ao seu branch local, ex: main).

Resultado: O branch de trabalho local é atualizado instantaneamente com as mudanças remotas, podendo gerar um commit de merge se o git merge for usado.

## Sintaxe
### Git Fetch
Bash

- Busca todas as branches do repositório remoto 'origin'
```git fetch origin```

- Busca apenas um branch específico do remoto

```git fetch origin <nome-do-branch>```

- Examina as diferenças entre o seu branch local e o remoto
```git log HEAD..origin/<nome-do-branch>```

### Git Pull
Bash

- Puxa e faz merge do branch <remoto>/<branch> no branch atual
```git pull <remoto> <branch>```

- Exemplo simples (o padrão é 'origin' e o branch atual)
```git pull```

- Puxa e faz rebase (opção mais limpa) em vez de merge
```git pull --rebase```

## Aplicação

Comando/ Aplicação Principal/ Benefício
- git fetch Inspeção Segura: Verificar o que aconteceu no remoto antes de aplicar as mudanças.Controle: Permite ao desenvolvedor decidir quando e como integrar as mudanças, evitando conflitos inesperados no código de trabalho.
- git pullAtualização Rápida: Sincronizar rapidamente um branch local com o remoto.Eficiência: Em ambientes com poucas divergências, economiza um passo ao combinar fetch e merge (ou rebase).

## Cuidados
- Git Fetch
Nenhuma alteração de código: Não há grandes riscos, pois o comando não toca no seu diretório de trabalho ou branch local.

Confusão: Lembre-se que as mudanças estão no branch de rastreamento remoto (origin/main), e não no seu branch local (main).

- Git Pull
Conflitos Imediatos: O git pull aplica as mudanças imediatamente. Se houver divergência entre o seu branch local e o remoto, ele gerará conflitos que você terá que resolver na hora.

Commits de Merge: A forma padrão (git pull sem --rebase) cria um commit de merge no histórico. Isso pode ser visto como "ruído" se for feito apenas para manter o branch atualizado. Para evitar isso, use git pull --rebase.

## Referência
- git fetch https://git-scm.com/docs/git-fetch
- git pull https://git-scm.com/docs/git-pull
# Git Commit
## Funcionamento

- O comando `git commit` registra no histórico do repositório todas as alterações que estão na staging area.
- Cada commit funciona como um snapshot do estado atual dos arquivos rastreados.*

Processo básico:

1. Modifica arquivos no diretório.
2. Usa git add para preparar as alterações.
3. Usa git commit para registrar a mudança com uma mensagem.
4. O commit recebe hash, autor, data e descrição.

Resultado: um histórico organizado, permitindo controle de versão eficiente.

## Sintaxe
## Commit simples
```bash
git commit -m "mensagem do commit"
```

## Commit com descrição detalhada
```bash
git commit
```


(abre o editor para escrever título e corpo)

## Adicionar e commitar ao mesmo tempo
```bash
git commit -am "mensagem"
```


(funciona apenas para arquivos já rastreados)

## Exemplo simples
```bash
git add index.html
git commit -m "Adiciona arquivo index.html"
```
## Exemplo avançado – commit com corpo
```bash
git commit -m "Ajusta validação do formulário" -m "Corrige bug ao validar email e adiciona novas regras para CPF."
```

## Aplicação

O `git commit` é utilizado para:

- Registrar alterações locais no histórico.
- Criar pontos de restauração.
- Facilitar revisão de código.
- Documentar o progresso do projeto.
- Manter o histórico limpo e compreensível.

## Boas práticas:

- Usar mensagens claras e objetivas.
- Título com até ~50 caracteres.
- Corpo explicando por que a mudança foi feita (opcional, recomendado).
- Fazer commits pequenos e focados.

## Cuidados

- Não commitar arquivos sensíveis ou grandes (usar .gitignore).
- Evitar commits enormes.
- Sempre revisar alterações com git status.
- Evitar mensagens vagas como “update”, “ajustes”, “testando”.

## Referência

[Git – Commit](https://git-scm.com/docs/git-commit)
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
# Git Log

O git log é um comando usado para exibir o histórico de commits de um repositório Git, listando-os em ordem cronológica inversa (do mais recente para o mais antigo). 
Git SCM

Ele permite filtrar quais commits mostrar por intervalo de revisões (usando notações como A..B ou A...B), por data (--since, --after), por autor ou por caminho de arquivo. 
Git SCM

Também é possível controlar a formatação da saída — por exemplo, com --pretty=oneline (resumo de cada commit em uma linha) ou exibir diffs de cada commit com -p. 
Git SCM

Outras opções úteis incluem:

--follow — para seguir o histórico de um arquivo mesmo após renomeações. 
Git SCM

--no-merges ou --merges — para filtrar commits que são (ou não são) merges. 
Git SCM

--max-count ou -n — para limitar quantos commits serão exibidos. 
Git SCM

## Principais usos:

Inspecionar o histórico de desenvolvimento.

Encontrar quando e por quem uma parte do código foi alterada.

Revisar mudanças específicas com diffs.

Investigar erros ou regressões ao identificar commits problemáticos.

## Exemplos de uso:

git log --no-merges — mostra todos os commits, exceto os de merge. 
Git SCM

git log --since="2 weeks ago" — lista commits feitos nas últimas duas semanas. 
Git SCM

git log --follow caminho/para/arquivo.txt — segue o histórico desse arquivo mesmo se ele foi renomeado. 
Git SCM

git log -p -m --first-parent — mostra os diffs para cada commit, para o ramo principal apenas, ignorando mudanças de ramos mesclados.
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
# d) git squash
## Funcionamento, sintaxe e aplicação do comando git squash
- O comando git squash altera o histórico de commits e os agrupa, permitindo um histórico limpo e apenas com os commits essenciais.

- É utilizado em conjunto com o comando `git rebase`, sendo necessário primeiro indicar quais commits sofrerão alteração e então adicionar a anotação `squash` no respectivo commit. 

Fluxo:
```
git rebase -i HEAD~2
```
Irá abrir o editor VIM para alteração dos commits.

<img src="readme-resources/squash.png" alt="Editor VIM">

Tendo adicionado a anotação `squash`, basta salvar, alterar a mensagem do commit e confirmar. 

Referência: [Youtube - 17. Juntando commits com squash - Git e Github na Vida Real](https://www.youtube.com/watch?v=UO2RFLAId7Y)
# Git cherry-pick
## Funcionamento, sintaxe e aplicação do comando git cherry-pick

### Funcionamento

Quando você executa o comando, o Git identifica as mudanças feitas naquele commit específico e tenta aplicá-las como um novo commit na branch em que você está trabalhando atualmente (HEAD).


Cópia, não referência: Um novo commit é criado com um novo ID (hash), o que significa que o commit original e a cópia são independentes. Se o commit original for alterado posteriormente, a cópia na outra branch não será afetada.

Conflitos: Se as alterações do commit selecionado entrarem em conflito com o código da branch atual, o Git pausará o processo para que você resolva os conflitos manualmente, de forma similar a um git merge ou git rebase.

Múltiplos Commits: É possível selecionar múltiplos commits de uma vez, e o Git os aplicará sequencialmente na ordem especificada. 

### Sintaxe:

```bash
 git cherry-pick <hash_do_commit>
```
### Aplicação:

O git cherry-pick é uma ferramenta poderosa para gerenciar o fluxo de trabalho do Git em cenários específicos, embora não deva substituir métodos como merge ou rebase na maioria dos casos.

- Hotfixes (Correções urgentes): É o caso de uso mais comum. Uma correção de bug urgente é feita em uma branch de desenvolvimento ou hotfix, e essa correção precisa ser aplicada imediatamente na branch principal (master ou main) sem mesclar todo o desenvolvimento em andamento.

- Aplicação seletiva de funcionalidades: Quando apenas uma parte das alterações em uma branch de funcionalidade (feature branch) está pronta para ser integrada em outra branch, o cherry-pick permite a aplicação pontual daquele commit específico.

- Evitar commits indesejados: Em vez de mesclar uma branch inteira que contém commits irrelevantes ou experimentais, você pode selecionar apenas os commits limpos e necessários.

- Restauração de alterações perdidas: Se commits foram acidentalmente removidos ou perdidos, o cherry-pick pode ser usado para reintroduzir essas alterações em uma branch ativa. 
# Git Rebase
## Funcionamento, sintaxe e aplicação do comando git rebase;

## Funcionamento
- O `git rebase` reaplica commits de um branch sobre outro, criando um histórico linear.
- Passos do processo:
  1. Identifica o ancestral comum entre os branches.
  2. Extrai os diffs dos commits do branch atual.
  3. Reseta o branch atual para a nova base.
  4. Aplica os diffs sobre a nova base.
- Resultado: mesmas mudanças, mas sem commits de merge desnecessários.

## Sintaxe

```bash
git checkout <branch>
git rebase <base>
```

### Exemplo simples

```bash
git checkout experiment
git rebase master
```

### Exemplo avançado com --onto

```bash
git rebase --onto master server client
```

**Significado:** reaplica os commits do branch `client` que divergiram de `server`, agora em cima de `master`.

## Aplicação

- Manter histórico limpo antes de enviar ao repositório remoto.
- Reorganizar commits de branches interdependentes.
- Evitar commits de merge desnecessários e facilitar revisão do código.

## Cuidados

- **Não rebase commits já compartilhados** (já enviados ao remoto), pois reescreve histórico.
- Pode gerar conflitos difíceis se outra pessoa baseou trabalho nos commits antigos.

## Referência

[Git - Rebase](https://git-scm.com/book/pt-br/v2/Branches-no-Git-Rebase)
