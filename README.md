# Guia de utilização do Docker

// comando para criar e subir container baseada na imagem passada no campo <image>
-- docker run <imagem>

// lista containers ativos
docker ps

// lista todos os containers, inativos inclusive
docker ps -a

// quando subir o container, quando a maquina local acessar porta 8080 é redirecionado para a porta 80 do container nginx
docker run -p 8080:80 nginx

// -d libera o terminal e mantém o container rodando
docker run -d -p 8080:80 nginx

// parar o container - usar id ou nome do container
docker stop <id/NomeContainer> 

// excluir container - usar id ou nome do container
docker rm <id/NomeContainer>  

// --name para nomear um container e facilitar interação
docker run --name <NomeContainer>  -d -p 8080:80 nginx

// executar comandos dentro do container
docker exec <id/NomeContainer>  ls

// entrar de forma interativa dentro do container, entrando dentro do container e executando comandos dentro dele
docker exec -it <id/NomeContainer> bash

// listar imagens da maquina
docker images



## Automatização da criação de containers e imagens
--> criando imagem dockerfile

// linguagem 
FROM golang:1.14

// arquivos que estao dentro da maquina, são copiados para o container
COPY . .

//gerar o build do codigo que está no main.go criado
RUN go build main.go

//Export a porta 8080 para conexão
EXPOSE 8080

// quando subir a imagem vai executar o main.go
ENTRYPOINT [ "./main" ]


// para criar a imagem -t = nome da imagem ; o ponto (.) significa que vai pegar do dockerfile
docker build -t anamalikovski/devfullcycle .

// cria e starta o container a partir da imagem criada
docker run -p 8080:8080 anamalikovski/devfullcycle

--> docker compose - gerenciamento de varios containers em um unico arquivo
//s ubir serviços de acordo com arquivo yaml
docker-compose up

version: '3'

// bloco de serviços
services: 
  nginx:
// image existente
    image: nginx
// aqui é diretório compartilhado, tudo que estiver dentro do ./nginx vai para o /usr/share/nginx/html do container -> evita que se for apagado o container vai perder os dados alterados nesse diretorio ./nginx     
volumes: 
      - ./nginx:/usr/share/nginx/html
// mesma questão das portas de apontamento: acessa local 8080 e redireciona para 80 dentro do container
    ports: 
      - 8080:80
