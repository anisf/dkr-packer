ARG ALPINE_VERSION

FROM alpine:${ALPINE_VERSION}

# Ansible versions : https://releases.hashicorp.com/packer/
ARG PACKER_VERSION
ENV PACKER_VERSION=${PACKER_VERSION}
LABEL packer_version=${PACKER_VERSION}

RUN apk update && apk upgrade \
    && apk add --no-cache --virtual .build-deps --update curl unzip \
    && apk add --no-cache --update git \
    && curl -LO https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip \
    && unzip '*.zip' -d /usr/local/bin \
    && apk del .build-deps \
    && rm -rf /var/cache/apk/* /tmp/* /root/.cache .build-deps *.zip\
    && adduser -S packer

USER packer
WORKDIR /home/packer

ENTRYPOINT ["/usr/local/bin/packer"]