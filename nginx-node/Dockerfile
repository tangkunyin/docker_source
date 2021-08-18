FROM nginx:stable

LABEL maintainer="Thomas Tang <thomas@tangkunyin.com>"
LABEL description="Based on the nginx:stable, node installed by nvm and nrm yarn all installed"

ENV NVM_VERSION 0.38.0
ENV NODE_VERSION 14.16.0

RUN  apt-get update && \
     apt-get install -y curl vim procps net-tools iputils-ping openssh-client openssh-server && \
     curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v${NVM_VERSION}/install.sh | bash && \
     export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")" && \
     [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" && \
     nvm install ${NODE_VERSION} && \
     nvm use ${NODE_VERSION} && \
     nvm alias default ${NODE_VERSION} && \
     npm install -g nrm yarn && \
     nrm use cnpm
CMD ["node"]