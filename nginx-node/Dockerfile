FROM nginx:stable

LABEL maintainer="Thomas Tang <thomas@tangkunyin.com>"
LABEL description="Based on the nginx:stable, node installed by nvm and nrm|pnpm|yarn were all installed"

ENV TZ Asia/Shanghai
ENV NVM_VERSION 0.39.1
ENV NODE_VERSION 16.13.2
ENV NVM_DIR /usr/local/nvm

COPY nginx.conf /etc/nginx

# Replace shell with bash first so we can source files
RUN  rm /bin/sh && ln -s /bin/bash /bin/sh && \
     ln -sf /usr/share/zoneinfo/$TZ /etc/localtime && echo '$TZ' > /etc/timezone && \
     apt-get update && \
     apt-get install -y curl vim procps && \
     mkdir -p /usr/local/nvm && \
     curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v${NVM_VERSION}/install.sh | bash && \
     . $NVM_DIR/nvm.sh && \
     nvm install ${NODE_VERSION} --default && \
     npm install -g nrm pnpm yarn && \
     nrm use taobao && \
     nvm cache clear && \
     rm -rf /var/lib/apt/lists/* && apt-get purge curl -y && apt-get autoremove -y && apt-get clean && apt-get autoclean && \
     ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log

ENV NODE_PATH $NVM_DIR/versions/node/v$NODE_VERSION/lib/node_modules
ENV PATH      $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

ENTRYPOINT nginx