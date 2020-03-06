FROM docker:stable
USER root
RUN apk update && apk add bash
RUN apk add --no-cache --virtual .build-deps g++ python3-dev libffi-dev openssl-dev && \
    apk add --no-cache --update python3 && \
    pip3 install --upgrade pip setuptools
# https://wiki.alpinelinux.org/wiki/How_to_get_regular_stuff_working
RUN apk add man man-pages mdocml-apropos less less-doc curl
RUN export PAGER=less
RUN apk add bash bash-doc bash-completion
RUN apk add util-linux pciutils usbutils coreutils binutils findutils grep git

RUN pip3 install pipenv
RUN apk add --update nodejs npm
ARG PULUMI_VERSION=v1.11.0
RUN apk update && \
    apk add --no-cache curl libc6-compat && \
    if [ "$PULUMI_VERSION" = "latest" ]; then \
      curl -fsSL https://get.pulumi.com/ | sh; \
    else \
      curl -fsSL https://get.pulumi.com/ | sh -s -- --version $(echo $PULUMI_VERSION | cut -c 2-); \
    fi


RUN curl -o aws-iam-authenticator https://amazon-eks.s3-us-west-2.amazonaws.com/1.14.6/2019-08-22/bin/linux/amd64/aws-iam-authenticator
RUN chmod +x ./aws-iam-authenticator
RUN mkdir -p $HOME/bin && cp ./aws-iam-authenticator $HOME/bin/aws-iam-authenticator

ENV PATH=$PATH:/root/.pulumi/bin:/root/bin


CMD bash

