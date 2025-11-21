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
