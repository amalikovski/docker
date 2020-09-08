# Guia básico de utilização do Docker

comando para criar e subir container baseado na imagem passada
`docker run <imagem>`

lista containers ativos
`docker ps`

lista todos os containers, inativos inclusive
`docker ps -a`

ao subir o container, quando a maquina local acessar a porta 8080 é redirecionado para a porta 80 do container nginx
`docker run -p 8080:80 nginx`

'-d' libera o terminal e mantém o container rodando
`docker run -d -p 8080:80 nginx`

parar o container - usar id ou nome do container
`docker stop <id/nomecontainer>`</id>

excluir container - usar id ou nome do container
`docker rm <id/nomecontainer>`</id>

'--name' para nomear um container e facilitar interação
`docker run --name nomecontainer -d -p 8080:80 nginx`

executar comandos dentro do container
`docker exec  <id/nomecontainer>  ls`</id>

entrar de forma interativa dentro do container, entrando dentro do container e executando comandos dentro dele
`docker exec -it  <id/nomecontainer> bash`</id>

listar imagens da maquina
`docker images`



## Automatização da criação de containers e imagens

### criando uma imagem a partir de um dockerfile

define a linguagem utilizada
`FROM golang:1.14`

arquivos que estao dentro da maquina, são copiados para o container
`COPY . .`

gerar o build do codigo que está no main.go criado
`RUN go build main.go`

expõe a porta 8080 para conexão
`EXPOSE 8080`

quando subir a imagem vai executar o main.go
`ENTRYPOINT [ "./main" ]`


para criar a imagem -t = nome da imagem. O ponto (.) significa que vai pegar a configuração do dockerfile

`docker build -t anamalikovski/devfullcycle .`


cria e starta o container a partir da imagem criada
`docker run -p 8080:8080 anamalikovski/devfullcycle`

### gerenciamento de varios containers em um unico arquivo atraves do docker compose

subir serviços de acordo com arquivo yaml
`docker-compose up`


**Comandos dentro do arquivo docker-compose.yaml**

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
