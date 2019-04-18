# Receita Firebase Command Line Tools

Esta receita pega a versão 8 do Nodejs para construir o ambiente porque é esta a versão que o Firebase usa hoje em dia.
A porta 9005 está exposta porque é a porta que o Firebase acessa para redirecionar a resposta do login.

## Build da imagem

Para fazer o build da imagem use o comando abaixo no local do Dockerfile.

```bash
docker build -f Dockerfile -t alexmsilva/firebase-tools .
```

## Login no Firebase

Após criar a imagem é necessário abrir um canal interativo com o bash do container e usar o commando login do Firebase.

```bash
docker run -p 9005:9005 -it alexmsilva/firebase-tools bash
```

## Commit do login

Até aqui, se tudo deu certo, é possível utilizar o firebase-tools sem problemas. Porém ao sair do container as informações de login serão perdidas e ao subir um novo container será necessário fazer todo o processo novamente.
Para evitar essa situação, é necessário fazer um commit com as alterções de login e adicioná-las na imagem.

Fora do container use o comando:

```bash
docker commit --message "Adds firebase login" id-do-container-logado alexmsilva/firebase-tools
```

Para testar se o login realmente deu certo, liste os projetos: por exemplo...

```bash
docker run -t --rm alexmsilva/firebase-tools firebase list
```

É só isso! Agora é só desfrutar do seu container, criar projetos, fazer deploys e tudo mais. Só não esqueça de montar o volume.
