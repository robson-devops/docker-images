# NodeJs 
Criação de imagem Docker para o build de projetos desenvolvidos em NodeJS.

Essa imagem poderá ser utilizada no Stage de Build de uma pipeline CI/CD.

A mesma precisará estar armazenada em um Registry público ou privado.

## Pré-requisitos

- Ter o [Docker](https://docs.docker.com/desktop/) instalado na máquina host.

## Criação da imagem
```bash
docker build --no-cache -t nodejs:latest -f Dockerfile .
```
