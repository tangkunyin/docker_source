FROM nginx:stable

LABEL maintainer="Thomas Tang <thomas@tangkunyin.com>"
LABEL description="Based on the nginx:stable, node installed by nvm and nrm|yarn|pnpm|git were all installed"

ENV NVM_VERSION 0.39.1
ENV NODE_VERSION 16.13.2
ENV NVM_DIR /usr/local/nvm

# Replace shell with bash first so we can source files
RUN  rm /bin/sh && ln -s /bin/bash /bin/sh && \  
     apt-get update && \
     apt-get install -y curl vim procps net-tools iputils-ping openssh-client openssh-server git && \
     rm -rf /var/lib/apt/lists/* && apt-get clean && apt-get autoclean && apt-get autoremove && \
     mkdir -p /usr/local/nvm && \
     ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log && \
     curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v${NVM_VERSION}/install.sh | bash && \
     . $NVM_DIR/nvm.sh && \
     nvm install ${NODE_VERSION} && \
     nvm alias default ${NODE_VERSION} && \
     nvm use ${NODE_VERSION} && \
     npm install -g nrm yarn pnpm && \
     nrm use taobao && \
     nvm cache clear

ENV NODE_PATH $NVM_DIR/versions/node/v$NODE_VERSION/lib/node_modules
ENV PATH      $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH
