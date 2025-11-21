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