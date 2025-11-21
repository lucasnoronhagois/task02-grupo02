info
asd
aaa

# g) Git Log

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