FROM nginx:stable

LABEL maintainer="Thomas Tang <thomas@tangkunyin.com>"
LABEL description="Based on the nginx:stable, node installed by nvm and nrm yarn all installed"


ENV NVM_VERSION 0.38.0
ENV NODE_VERSION 14.16.0

# Replace shell with bash first so we can source files
RUN  rm /bin/sh && ln -s /bin/bash /bin/sh && \  
     apt-get update && \
     apt-get install -y curl vim procps net-tools iputils-ping openssh-client openssh-server && \
     rm -rf /var/lib/apt/lists/* && \
     curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v${NVM_VERSION}/install.sh | bash && \
     export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")" && \
     [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" && \
     nvm install ${NODE_VERSION} && \
     nvm alias default ${NODE_VERSION} && \
     nvm use ${NODE_VERSION} && \
     npm install -g nrm yarn && \
     nrm use cnpm && \
     nvm cache clear

ENV NODE_PATH $NVM_DIR/versions/node/v$NODE_VERSION/lib/node_modules
ENV PATH      $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH