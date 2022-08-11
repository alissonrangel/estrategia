# Aula Docker

## Figuras para a aula

![alt Figura 1](imgs/docker.png)
https://d2iq.com/blog/docker-vs-kubernetes-vs-apache-mesos


![alt Figura 2](https://docs.docker.com/images/Container%402x.png)

![alt Figura 3](https://docs.docker.com/images/VM%402x.png)










## Nginx

* docker run nginx:alpine
* -d
* docker logs -f
* --rm
* -it
* exec

* /etc/nginx/conf
  
* alterar pagina inicial
* remvover container
* iniciar novo container
* alterar pagina inicial
* parar container
* start containe
* criando uma nova imagem com nosso index - docker commit


> Fazer revisão até slide 46


## criando nova imagem nginx com vim e index alterado

* passando index por copy
  * /usr/share/nginx/html/index.html
* Depois fazer com mapeamento de volume passando o index lá pra dentro


## Hello world

* https://hub.docker.com/_/hello-world

* docker run alpine:latest "echo" "Hello, World"

## Java

* Hello World Java

* criando nossa imagem java com alpine

* alterando nosso hello world java para nossa imagem


## Node
* npm install --sever


## Comandos Básicos

* docker info
* docker ps
* docker ps -a
* docker images ls
* docker build . -t 
* docker run
* docker pull
  * ports
  * volumes
  * daemon

* docker stop
* docker start
    * explicar o stateless aqui
* docker network create
dsdsdsd

### compartilhando volume do host com o container

- docker run ... -> cria novos containers
- docker run nginx
- docker run -p 8000:80 nginx -> cria container que tem a porta 80 do container mapeado para a 8000 do host
- docker run -d -p 8000:80 nginx -> não trava o teclado

- Com o container rodando:
- docker exec -it {id_do_cont} bash -> entra no SO do container
  - apt-get update
  - apt-get install vim

- docker commit {id_do_cont} {nome_da_nova_image} -> cria uma nova imagem com as alterações feitas no container

### Dockerfile

```
FROM nginx:latest

RUN apt-get update -y
RUN apt-get install vim -y

COPY index.html /usr/share/nginx/html/

RUN ls -la /usr/share/nginx/html/
```
- docker build . -t nginx-coruja -> cria uma image a partir do Dockerfile

- docker run -p 5000:80 nginx-coruja -> cria container que tem a porta 80 do container mapeado para a 5000 do host
- docker build . -t nginx-coruja-sem-index

- Mapeamento de Volumes -> Um volume local no host pode compartilhar com um volume dentro do container
- docker run -p 5000:80 -v $(pwd):/usr/share/nginx/html nginx-coruja-sem-index  

## Docker-compose
