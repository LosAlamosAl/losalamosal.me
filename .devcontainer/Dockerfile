FROM debian:buster-slim

RUN adduser --home /home/devboy --shell /usr/bin/zsh --no-create-home devboy \
    && usermod -aG sudo devboy \
    && mkdir /home/devboy \
    && chown devboy /home/devboy \
    && chgrp devboy /home/devboy

# Had to update certificates--git https clone was failing
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends bash zsh zip unzip less wget curl git jq htop gnupg2 ssh openssh-client ca-certificates \
    && update-ca-certificates \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# From https://github.com/microsoft/vscode-dev-containers/tree/main/containers/hugo
# VARIANT can be either 'hugo' for the standard version or 'hugo_extended' for the extended version.
ARG VARIANT=hugo
# VERSION can be either 'latest' or a specific version number
ARG VERSION=latest

# Download Hugo
RUN apt-get update && apt-get install -y ca-certificates openssl git curl && \
    rm -rf /var/lib/apt/lists/* && \
    case ${VERSION} in \
    latest) \
    export VERSION=$(curl -s https://api.github.com/repos/gohugoio/hugo/releases/latest | grep "tag_name" | awk '{print substr($2, 3, length($2)-4)}') ;;\
    esac && \
    echo ${VERSION} && \
    wget -O ${VERSION}.tar.gz https://github.com/gohugoio/hugo/releases/download/v${VERSION}/${VARIANT}_${VERSION}_Linux-64bit.tar.gz && \
    tar xf ${VERSION}.tar.gz && \
    mv hugo /usr/bin/hugo

# Hugo dev server port
EXPOSE 1313

USER devboy
WORKDIR /home/devboy
RUN zsh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" || true
RUN git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

# Oh My ZSH installs a .zshrc. Remove so we can overwrite it when cloning dotfiles.
RUN rm ~/.zshrc

#ENV SHELL /bin/zsh    THIS IS WRONG
