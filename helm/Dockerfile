FROM alpine:3.22

# Install necessary dependencies
# Install required dependencies
RUN apk update && apk add --no-cache \
    curl \
    ca-certificates \
    bash \
    gnupg \
    && rm -rf /var/cache/apk/*

ENV HELM_VERSION=v3.18.5
ENV KUBECTL_VERSION=v1.30.1

RUN curl -LO https://dl.k8s.io/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl && \
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

# Install Helm
RUN curl https://get.helm.sh/helm-${HELM_VERSION}-linux-amd64.tar.gz -o helm.tar.gz \
    && tar -zxvf helm.tar.gz \
    && mv linux-amd64/helm /usr/local/bin/helm \
    && rm -rf helm.tar.gz linux-amd64

# Verify Helm installation
#RUN helm version

# Default command
ENTRYPOINT ["helm"]

