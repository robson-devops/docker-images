FROM alpine:latest as build
LABEL org.opencontainers.image.authors="br.robsonferreira@gmail.com.br"

ARG NODEJS_VERSION=v22.2.0
# Ref.: https://nodejs.org/dist/

RUN apk update && \ 
    apk add --no-cache \
        zlib-dev=1.3.1-r1 \
        curl=8.11.0-r2 && \
    curl -fsSL -o /tmp/nodejs.tar.xz https://nodejs.org/dist/${NODEJS_VERSION}/node-${NODEJS_VERSION}-linux-x64.tar.xz && \
    tar -xJf /tmp/nodejs.tar.xz -C /usr/bin/ && \
    mv /usr/bin/node-${NODEJS_VERSION}-linux-x64 /usr/bin/nodejs

FROM ubuntu:18.04

COPY --from=build /usr/bin/nodejs /usr/bin/nodejs 

WORKDIR /nodejs

#COPY . .

ENV PATH $PATH:/usr/bin/nodejs/bin

CMD ["npm","--version"]