FROM ghcr.io/linuxserver/baseimage-ubuntu:arm64v8-focal

ENV HOME="/config"

# dependencies
RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - && \
    echo 'deb https://deb.nodesource.com/node_14.x focal main' \
      > /etc/apt/sources.list.d/nodesource.list && \
    apt-get update && \
    apt-get install -y git build-essential nodejs jq libatomic1 net-tools sudo autoconf libtool bison re2c libxml2-dev

# Download PHP source
RUN curl -fsSL -o php.tar.gz https://www.php.net/distributions/php-7.0.33.tar.gz && \
    tar -xvzf php.tar.gz

# Compile PHP
RUN cd php-7.0.33 && \
    ./configure && \
    make -j $(nproc) && \
    make install && \
    cd .. && \
    rm -rf php-7.0.33

# install code-server
RUN if [ -z ${CODE_RELEASE+x} ]; then \
      CODE_RELEASE=$(curl -sX GET https://api.github.com/repos/coder/code-server/releases/latest \
      | awk '/tag_name/{print $4;exit}' FS='[""]' | sed 's|^v||'); \
    fi && \
    mkdir -p /app/code-server && \
    curl -o \
      /tmp/code-server.tar.gz -L \
      "https://github.com/coder/code-server/releases/download/v${CODE_RELEASE}/code-server-${CODE_RELEASE}-linux-arm64.tar.gz" && \
    tar xf /tmp/code-server.tar.gz -C \
      /app/code-server --strip-components=1 && \
    echo "**** patch 4.0.2 ****" && \
    if [ "${CODE_RELEASE}" = "4.0.2" ] && [ "$(uname -m)" !=  "x86_64" ]; then \
      cd /app/code-server && \
      npm i --production @node-rs/argon2; \
    fi

# install composer
RUN curl -o /usr/bin/composer -L https://getcomposer.org/download/latest-2.2.x/composer.phar && \
    chmod +x /usr/bin/composer

# clean up
RUN apt-get purge --auto-remove -y build-essential nodejs && \
    apt-get clean && \
    rm -rf \
      /config/* \
      /tmp/* \
      /var/lib/apt/lists/* \
      /var/tmp/* \
      /etc/apt/sources.list.d/nodesource.list \
      /php.tar.gz

# add local files
COPY /root /

# ports and volumes
EXPOSE 8443
