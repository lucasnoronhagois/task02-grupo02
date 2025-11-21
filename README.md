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