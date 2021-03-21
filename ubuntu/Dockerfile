ARG UBUNTU_VERSION

FROM ubuntu:${UBUNTU_VERSION} AS builder

# Ansible versions : https://releases.hashicorp.com/packer/
ARG PACKER_VERSION
ENV PACKER_VERSION=${PACKER_VERSION}
LABEL packer_version=${PACKER_VERSION}

RUN apt update \
    && apt install -y curl unzip \
    && curl -LO https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip \
    && unzip '*.zip' -d /usr/local/bin

FROM ubuntu:${UBUNTU_VERSION}

COPY --from=builder /usr/local/bin/packer /usr/local/bin

RUN useradd --system packer

USER packer
WORKDIR /home/packer

ENTRYPOINT ["/usr/local/bin/packer"]