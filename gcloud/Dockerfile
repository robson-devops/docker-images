FROM alpine:3.19 AS builder

ARG CLOUD_SDK_VERSION=461.0.0

ENV CLOUD_SDK_VERSION=$CLOUD_SDK_VERSION
ENV PATH /google-cloud-sdk/bin:$PATH

RUN addgroup -g 1000 -S cloudsdk && \
    adduser -u 1000 -S cloudsdk -G cloudsdk

RUN apk update && \
    apk add --no-cache \
        curl=8.11.0-r2 \
        python3=3.11.6-r1 \
        py3-crcmod=1.7-r10 \
        py3-openssl=23.3.0-r0 \
        bash=5.2.21-r0 \
        libc6-compat=1.1.0-r4 \
        openssh-client=9.6_p1-r0 \
        git=2.43.0-r0 \
        grep=3.11-r0 \
        gnupg=2.4.4-r0 && \
    curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    tar xzf google-cloud-cli-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    rm google-cloud-cli-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    rm -rf /google-cloud-sdk/bin/anthoscli && \
    rm -rf /google-cloud-sdk/bin/bq && \
    gcloud config set core/disable_usage_reporting true && \
    gcloud config set component_manager/disable_update_check true && \
    gcloud config set metrics/environment github_docker_image && \
    gcloud --version

FROM alpine:3.19 

ENV PATH /google-cloud-sdk/bin:$PATH

RUN apk update && apk add --no-cache python3=3.11.6-r1 

COPY --from=builder /google-cloud-sdk/bin/ /google-cloud-sdk/bin/
COPY --from=builder /google-cloud-sdk/lib/ /google-cloud-sdk/lib/

VOLUME ["/root/.config"]
