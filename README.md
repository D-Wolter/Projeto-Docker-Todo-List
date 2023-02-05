# :whale2: Projeto Docker To do List :whale2:

Para colocarmos em prática o aprendizado da primeira seção de back-end nos foi proposto este projeto em que colocamos em prática os comandos para criação de imagens e containers. 
O objetivo do projeto foi dockerizar a aplicação Todo App que já estava pronta. Para isso desenvolvemos arquivos Dockerfile e um arquivo docker-compose.

## O aplicativo Todo App
É um aplicativo de tarefas em que é possível organizar em uma lista o que precisa ser realizado. É possível adicionar, marcar e/ou remover suas tarefas.

![intro](https://user-images.githubusercontent.com/106452876/213876138-134df37f-18ad-439d-8c90-d433cdd5db54.gif)

## Tecnologias usadas
Back-end:
> Desenvolvido usando: Docker, docker-compose

## Instalando Dependências
> Frontend
```bash
cd ./todo-app/front-end
npm install
``` 
> Backend
```bash
cd ./todo-app/back-end
npm install
``` 
> Testes

:warning: Essa aplicação só funciona se associada a uma rede Docker;

## Executando aplicação
* Para rodar o front-end:

  ```
    cd ./todo-app/front-end && npm start
  ```
* Para rodar o back-end:

  ```
    cd ./todo-app/back-end && npm start
  ```
  
## Executando Testes

* Para rodar todos os testes:

  ```
    npm test
  ```
## Dockerfile
Para dockerizar a aplicação, foram criados três Dockerfile. Um para back-end, outro para front-end e outro para testes.
* Back-end:

  ```js
    FROM node:14-alpine
    WORKDIR /docker
    ADD ./node_modules.tar.gz .
    COPY . .
    EXPOSE 3001
    CMD ["npm", "start"]
  ```
* Front-end:

  ```js
    FROM node:14-alpine
    WORKDIR /docker
    ADD ./node_modules.tar.gz .
    COPY . .
    EXPOSE 3000
    CMD ["npm", "start"]
  ```
* Testes:

  ```js
    FROM mjgargani/puppeteer:trybe1.0
    WORKDIR /docker
    ADD ./node_modules.tar.gz .
    COPY . .
    CMD ["npm", "test"]
  ```
  :warning: Foi utilizado o ADD pois era preciso descompactar o arquivo ```node_modules.tar.gz``` e adicioná-lo em seguida no WORKDIR através do COPY.
  
  ## docker-compose
  ```js
    version: '3'
    services:
    todoback:
      build: ./todo-app/back-end
      ports: 
        - 3001:3001
    todofront:
    build: ./todo-app/front-end
    environment:
      - REACT_APP_API_HOST=todoback
    ports: 
      - 3000:3000
    depends_on:
      - todoback
    todotests: 
    build: ./todo-app/tests
    environment:
      - FRONT_HOST=todofront
    depends_on:
      - todoback
      - todofront
  ```
  
