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
RUN apk add util-linux pciutils usbutils coreutils binutils findutils grep

RUN pip3 install pipenv
RUN apk add --update nodejs npm
ARG PULUMI_VERSION=v1.11.0

ENV PATH=$PATH:/root/.pulumi/bin

RUN apk update && \
    apk add --no-cache curl libc6-compat && \
    if [ "$PULUMI_VERSION" = "latest" ]; then \
      curl -fsSL https://get.pulumi.com/ | sh; \
    else \
      curl -fsSL https://get.pulumi.com/ | sh -s -- --version $(echo $PULUMI_VERSION | cut -c 2-); \
    fi

CMD bash

