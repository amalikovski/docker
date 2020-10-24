<h1 align="center">Guia Docker</h1>
<p align="center"> Projeto com guia básico de utilização do Docker </p>
<p align="center"> 🚧  Em constante construção 🚧
<p align="center"><img src="https://img.shields.io/static/v1?label=Docker&message=Guia&logoColor=white&labelColor=066DA5&color=5a5e60&style=for-the-badge&logo=docker" /></p>

## Tabela de Conteúdos

- [Guia de Utilização Docker](#guia)
  - [Comandos para gerenciamento dos container](#comandos)
  - [Automatização do gerenciamento de containers](#automatizacao)
    - [Criar uma imagem utilizando o dockerfile](#dockerfile)
    - [Gerenciamento de containers utilizando o docker compose](#dockerfile)
- [Tecnologias](#tecnologias)
- [Autor](#autor)

<h4>Guia de Utilização Docker</h4>

<h5 id="comandos">Comandos para gerenciamento dos container</h5>

-> comando para criar e subir container baseado na imagem passada
`docker run <imagem>`

-> comando para listar containers ativos
`docker ps`

-> comando para listar todos os containers, inativos inclusive
`docker ps -a`

-> comando para subir o container e quando a maquina local acessar a porta 8080 é redirecionado para a porta 80 do container 'nginx' criado
`docker run -p 8080:80 <id/nomecontainer>`

-> comando para subir o container e quando a maquina local acessar a porta 8080 é redirecionado para a porta 80 do container criado e adicionando '-d' libera o terminal e mantém o container rodando
`docker run -d -p 8080:80 <id/nomecontainer>`

-> comando para parar o container - usar id ou nome do container
`docker stop <id/nomecontainer>`</id>

-> comando para excluir container - usar id ou nome do container
`docker rm <id/nomecontainer>`</id>

-> comando para criar um container a partir de uma imagem e utilizando o '--name' para nomear um container e facilitar interação
`docker run --name <nomecontainer> -d -p 8080:80 nginx`

-> comando para executar comandos dentro do container
`docker exec  <id/nomecontainer>  ls`</id>

-> comando para entrar de forma interativa dentro do container, entrando dentro do container e executando comandos dentro dele
`docker exec -it  <id/nomecontainer> bash`</id>

-> comando para listar imagens da maquina
`docker images`

<h5 id="automatizacao">Automatização da criação de containers e imagens</h5>

<h6 id="dockerfile">Criar uma imagem utilizando o dockerfile</h6>

<a href="https://github.com/amalikovski/docker/blob/master/Dockerfile">Visualizar arquivo de exemplo de DockerFile</a>

-> para definir a linguagem utilizada
`FROM golang:1.14`

-> para copiar arquivos que estao dentro da maquina local para o container
`COPY . .`

-> para gerar o build do codigo que está no main.go criado
`RUN go build main.go`

-> para expor a porta 8080 para conexão
`EXPOSE 8080`

-> para quando subir o container com a imagem executar o main.go
`ENTRYPOINT [ "./main" ]`

-> para criar a imagem -t = nome da imagem. O ponto (.) significa que vai pegar a configuração do dockerfile
`docker build -t anamalikovski/devfullcycle .`

-> para criar cria e starta o container a partir da imagem criada
`docker run -p 8080:8080 anamalikovski/devfullcycle`

<h6 id="compose">Gerenciamento de containers utilizando o docker compose</h6>

-> para subir serviços de acordo com arquivo yaml
`docker-compose up`

<p>Comandos dentro do arquivo docker-compose.yaml</p>

`version: '3'`

bloco de serviços

```services:nginx:
services: 
  nomeDoContainer:
    image: nginx
    volumes: 
      - ./nginx:/usr/share/nginx/html
    ports: 
      - 8080:80
```

image existente

`image: nginx`

aqui é diretório compartilhado, tudo que estiver dentro do ./nginx vai para o /usr/share/nginx/html do container -> evita que se for apagado o container vai perder os dados alterados nesse diretorio ./nginx
`volumes:`

`- ./nginx:/usr/share/nginx/html`
mesma questão das portas de apontamento: acessa local 8080 e redireciona para 80 dentro do container
`ports:`

`- 8080:80`

<h5 id="tecnologias">Tecnologias </h5>
<p> As tecnologias abaixo foram utilizadas neste guia</p>

<ul><li><a href="https://www.docker.com">Docker</a></li>

<li><a href="https://yaml.org">Yaml - Linguagem utilizada no arquivo DockerFile<a></li>
<li><a href="http://www.golangbr.org">Go - Linguagem utilizada no arquivo main.go</a></li></ul>

<h5 id="autor">Autor </h5>

<a href="https://www.linkedin.com/in/anamalikovski/">
<img style="border-radius: 50%;" src="./assets/autor.jpg" width="100px;" alt="Ana Malikovski"/>
<br />
<sub><b>Ana Malikovski</b></sub></a>

👋🏽 Entre em contato!
[![Linkedin Badge](https://img.shields.io/badge/-Ana-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/anamalikovski/)](https://www.linkedin.com/in/anamalikovski/)
[![Gmail Badge](https://img.shields.io/badge/-amalikovski@gmail.com-c14438?style=flat-square&logo=Gmail&logoColor=white&link=mailto:amalikovski@gmail.com)](mailto:amalikovski@gmail.com)

