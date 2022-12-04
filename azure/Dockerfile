# TODO - supprimer de nyx-meushi
FROM debian:bullseye-slim
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
      && DEBIAN_FRONTEND=noninteractive apt-get install --yes --no-install-recommends \
        vim git curl python3 \
        gnupg

RUN curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add - && \
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-bullseye-prod bullseye main" > /etc/apt/sources.list.d/microsoft.list  && \
    apt-get update && apt-get install -y azure-cli powershell

RUN useradd --create-home --shell /bin/bash --uid 1000 viny

USER viny
WORKDIR /home/viny