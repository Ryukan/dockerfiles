FROM alpine:3.20

RUN apk add --no-cache curl

ENV KUBECTL_VERSION=v1.30.1

## Disable if you are not using minikube
ARG MINIKUBE_PATH
RUN mkdir -p ${MINIKUBE_PATH}/.minikube
##

RUN curl -LO https://dl.k8s.io/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl && \
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

ENTRYPOINT ["kubectl"]
