# NodeJs

Criação de imagem Docker para o build de projetos desenvolvidos em NodeJS.
Essa imagem poderá ser utilizada no Stage de Build de uma pipeline CI/CD.
A mesma precisará estar armazenada em um Registry público ou privado.

Fonte: https://nodejs.org/api/cli.html

## Pré-requisitos

- Ter o [Docker](https://docs.docker.com/desktop/) instalado na máquina host.

## Criação da imagem

```bash
docker build --no-cache -t nodejs:latest -f Dockerfile .
docker run -it --name nodejs $(docker images | grep nodejs | awk '{ print $3 }') sh
```
<div align="center"><center><h6>:rocket: Go Devops... !!!</center></div>