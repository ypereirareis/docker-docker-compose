FROM docker:latest


# Install tzdata and change to Europe/Paris
RUN  set -x && \
    apk --update add tzdata && \
    ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime && \
    date && \
    rm -rf /var/cache/apk/*


# Install tools...
RUN set -x && \
    apk --update add \
      ca-certificates \
      curl \
      make \
      nano \
      gcc \
      wget \
      openssh \
      openssh-client \
      bash \
      git \
    && rm -rf /var/cache/apk/*


# Install glibc on Alpine (required by docker-compose) from
# https://github.com/sgerrand/alpine-pkg-glibc
# See also https://github.com/gliderlabs/docker-alpine/issues/11
RUN set -x && \
    GLIBC_VERSION='2.23-r3' && \
    curl -Lo /etc/apk/keys/sgerrand.rsa.pub https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub && \
    curl -Lo glibc.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/$GLIBC_VERSION/glibc-$GLIBC_VERSION.apk && \
    curl -Lo glibc-bin.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/$GLIBC_VERSION/glibc-bin-$GLIBC_VERSION.apk && \
    apk update && \
    apk add glibc.apk glibc-bin.apk && \
    rm -rf /var/cache/apk/* glibc.apk glibkc-bin.apk

# Install docker-compose
# https://docs.docker.com/compose/install/
RUN set -x && \
    DOCKER_COMPOSE_URL=https://github.com$(curl -L https://github.com/docker/compose/releases/latest | grep -Eo 'href="[^"]+docker-compose-Linux-x86_64' | sed 's/^href="//') && \
    curl -Lo /usr/local/bin/docker-compose $DOCKER_COMPOSE_URL && \
    chmod a+rx /usr/local/bin/docker-compose

# Print info to check if everything is OK
RUN set -x && \
    ( docker version || true ) && \
    docker-compose version && \
    make -v && \
    gcc -v && \
    date
