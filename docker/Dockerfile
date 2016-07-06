FROM opsidian/alpine-base:latest

ENV TERRAFORM_BUILD_TAG=v0.6.16

RUN \
    echo "Install packages" \
    && apk add --no-cache \
      go git zip \

    && echo "Install Terraform" \
    && mkdir /tmp/go \
    && export GOPATH=/tmp/go PATH="/tmp/go/bin:$PATH" \
    && go get github.com/hashicorp/terraform \
    && cd /tmp/go/src/github.com/hashicorp/terraform \
    && git checkout ${TERRAFORM_BUILD_TAG} \
    && XC_OS="linux" XC_ARCH="amd64" make bin \
    && mv /tmp/go/bin/terraform* /bin/ \

    && echo "Clean up" \
    && apk del go git zip \
    && rm -rf /tmp/*

COPY opsidian-release /etc/opsidian-release
