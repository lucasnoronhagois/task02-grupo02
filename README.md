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