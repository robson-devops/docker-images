FROM alpine:3.20.3 AS builder

ARG CLOUD_SDK_VERSION=502.0.0

ENV CLOUD_SDK_VERSION=$CLOUD_SDK_VERSION
ENV PATH /google-cloud-sdk/bin:$PATH

RUN addgroup -g 1000 -S cloudsdk && \
    adduser -u 1000 -S cloudsdk -G cloudsdk

RUN apk update && \
    apk add --no-cache \
        curl \
        python3 \
        py3-crcmod \
        py3-openssl \ 
        libc6-compat \
        openssh-client \
        grep \
        gnupg && \
    curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    tar xzf google-cloud-cli-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    rm google-cloud-cli-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    rm -rf /google-cloud-sdk/bin/anthoscli && \
    rm -rf /google-cloud-sdk/bin/bq && \
    gcloud config set core/disable_usage_reporting true && \
    gcloud config set component_manager/disable_update_check true && \
    gcloud config set metrics/environment github_docker_image && \
    gcloud --version

FROM alpine:3.20.3 

ENV PATH /google-cloud-sdk/bin:$PATH

RUN apk update && apk add --no-cache python3 

COPY --from=builder /google-cloud-sdk/bin/ /google-cloud-sdk/bin/
COPY --from=builder /google-cloud-sdk/lib/ /google-cloud-sdk/lib/

VOLUME ["/root/.config"]
