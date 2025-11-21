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
