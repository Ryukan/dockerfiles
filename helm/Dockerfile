FROM kubectl:1.30.1



ENV HELM_VERSION=v3.18.5


# Install Helm
RUN curl https://get.helm.sh/helm-${HELM_VERSION}-linux-amd64.tar.gz -o helm.tar.gz \
    && tar -zxvf helm.tar.gz \
    && mv linux-amd64/helm /usr/local/bin/helm \
    && rm -rf helm.tar.gz linux-amd64

# Verify Helm installation
#RUN helm version

# Default command
ENTRYPOINT ["helm"]
