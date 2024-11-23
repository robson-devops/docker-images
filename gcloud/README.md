# Google Cloud CLI

**EM CONSTRUÇÃO...**  

Criação de imagem Docker para a administração dos recursos computacionais GCP via linha de comando.
Essa imagem poderá ser utilizada no Stage de Deploy de uma pipeline CI/CD.
A mesma precisará estar armazenada em um Registry público ou privado.

Fonte: https://cloud.google.com/cli?hl=pt-BR

## Pré-requisitos

- Ter o [Docker](https://docs.docker.com/desktop/) instalado na máquina host.

## Criação da imagem

```bash
docker build --no-cache -t gcloud-sdk:latest -f Dockerfile . 
docker run -it --name nodejs $(docker images | grep nodejs | awk '{ print $3 }') sh 
```
<div align="center"><center><h6>:rocket: Go Devops... !!!</center></div>