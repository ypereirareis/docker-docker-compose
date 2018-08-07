FROM tmaier/docker-compose

# Install tools...
RUN set -x && \
    apk --no-cache add \
      ca-certificates \
      git \
      openssh \
      openssh-client \
      wget \
      curl \
      make \
      bash

# Print info to check if everything is OK
RUN set -x && \
    ( docker version || true ) && \
    docker-compose version && \
    make -v
